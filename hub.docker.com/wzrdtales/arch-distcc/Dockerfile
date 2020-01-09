FROM base/archlinux

RUN pacman -Sy && pacman -S base-devel distcc --noconfirm

CMD "distccd" "--allow=0.0.0.0/0" "--daemon" "--verbose" "--no-detach"
