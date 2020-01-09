FROM clearlinux:latest
RUN swupd update
RUN swupd bundle-add os-clr-on-clr
RUN useradd clear && \
    usermod -G wheel -a clear && \
    echo "%wheel ALL=(ALL) NOPASSWD: ALL" | EDITOR='tee -a' visudo
