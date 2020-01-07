FROM alpine:latest AS build
ADD https://mirrors.kernel.org/archlinux/iso/latest/archlinux-bootstrap-2017.07.01-x86_64.tar.gz .
RUN tar -xzf archlinux-bootstrap-2017.07.01-x86_64.tar.gz

FROM scratch
COPY --from=build root.x86_64 /
RUN pacman-key --init && \
  pacman-key --populate archlinux && \
  echo 'Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch' >> /etc/pacman.d/mirrorlist && \
  pacman -Syyu --noconfirm
