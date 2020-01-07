FROM zaoqi/archlinux-rolling
RUN pacman -Syu --noconfirm && yes | pacman -Scc && rm -fr /var/lib/pacman/sync/*

FROM scratch
COPY --from=0 / /
