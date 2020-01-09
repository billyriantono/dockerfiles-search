FROM archlinux/base

RUN useradd -m yay
RUN pacman -Syuq --needed --noconfirm
RUN pacman -Sq --needed --noconfirm git go sudo base-devel
RUN mkdir -p /opt/Workspace
RUN chown -R yay.yay /opt/Workspace

RUN printf 'yay ALL=(ALL) NOPASSWD: ALL\n' | tee -a /etc/sudoers

USER yay
RUN git clone https://aur.archlinux.org/yay.git /opt/Workspace/yay
RUN cd /opt/Workspace/yay && makepkg -si --noconfirm

CMD ["/usr/lib/systemd/systemd"]
