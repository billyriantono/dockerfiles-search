FROM rafalwcode/archbase

ARG date

ENV server="https://archive.archlinux.org"

RUN echo "Server = $server/repos/$(date -d $date +%Y/%m/%d)/\$repo/os/\$arch/" > /etc/pacman.d/mirrorlist && \
    pacman -Syyu --noconfirm && \
    (/bin/yes Y | pacman -Scc) && \
    rm -rf /usr/share/man

ENTRYPOINT ["/usr/bin/bash"]
