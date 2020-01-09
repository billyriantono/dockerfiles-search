FROM pritunl/archlinux
# MAINTAINER: gray380

# Rebuild keys
RUN pacman -S archlinux-keyring --noconfirm \
	&& pacman-key --populate archlinux \
	&& pacman-key --refresh

# Update system
RUN pacman -Syu --noconfirm

# Create user 'contusr'
RUN ugid='880016' \ 
    && groupadd --gid "${ugid}" contgrp \
    && useradd --uid "${ugid}" --gid "${ugid}" --shell /usr/bin/false contusr

RUN groupadd wheel

# Install Lightweight HTTP server and IMAP/POP3 proxy server, mainline release
# and enable coresponding systemd service
RUN pacman -S nginx-mainline --noconfirm \
	&& pacman -S base-devel git sudo --noconfirm \
	&& find /var/cache/pacman/pkg -mindepth 1 -delete \
	&& setcap 'cap_net_bind_service=ep' /usr/bin/nginx \
	&& chown --recursive contusr:contgrp /var/lib/nginx /var/log/nginx \
	&& install --directory --owner=contusr --group=contgrp --mode=700 /run/nginx

# Clear cache
RUN pacman -Scc --noconfirm

# Add yaourt user
RUN chmod 640 /etc/sudoers && echo '%wheel ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && chmod 440 /etc/sudoers && useradd -m -p321321 -G wheel yaourt

# Add yaourt
RUN sudo -u yaourt rm -rf /tmp/package-query \
    && sudo -u yaourt rm -rf /tmp/yaourt \
    && cd /tmp \
    && sudo -u yaourt git clone https://aur.archlinux.org/package-query.git \
    && cd /tmp/package-query \
    && yes | sudo -u yaourt makepkg -si \
    && cd .. \
    && sudo -u yaourt git clone https://aur.archlinux.org/yaourt.git \
    && cd /tmp/yaourt \
    && yes | sudo -u yaourt makepkg -si \
    && cd .. \
    && echo 'EXPORT=2' >> /etc/yaourtrc \
    && yaourt --version

# Install Lua script engine module for mainline nginx
RUN yaourt -Ss nginx-mainline-mod-lua --noconfirm

USER contusr
VOLUME ["/var/lib/nginx"]
EXPOSE 80/tcp 443/tcp
ENTRYPOINT ["/usr/bin/nginx", "-g", "daemon off;"]
