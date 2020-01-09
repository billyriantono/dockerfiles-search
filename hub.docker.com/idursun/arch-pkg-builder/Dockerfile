FROM archlinux
RUN pacman -Sy --noconfirm
RUN pacman -S --noconfirm archlinux-keyring 
RUN pacman -S --noconfirm devtools binutils fakeroot
RUN useradd -m -g wheel builder
USER builder
