FROM archlinux/base AS builder
RUN pacman -Syu --noconfirm
RUN pacman -S --noconfirm --needed base-devel git sudo
RUN groupadd -g 9999 yay
RUN useradd -u 9999 -g yay -m yay
RUN echo 'yay ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/yay
RUN sudo -u yay git clone https://aur.archlinux.org/yay.git /tmp/yay
RUN cd /tmp/yay && sudo -u yay makepkg -s --noconfirm --rmdeps

FROM archlinux/base
COPY --from=builder /tmp/yay/yay-*.pkg.tar.xz /tmp/yay/
RUN set -ex \
 && pacman -Syu --noconfirm \
 && pacman -U --noconfirm /tmp/yay/yay-*.pkg.tar.xz \
 && pacman -S --noconfirm --needed sudo pacman-contrib cronie \
 && pacman -Scc
RUN rm -rf /tmp/*

RUN groupadd -g 9999 yay
RUN useradd -u 9999 -g yay -m yay
RUN echo 'yay ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/yay

COPY checkupdates.sh /
RUN chmod +x /checkupdates.sh

COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["checkupdates"]
