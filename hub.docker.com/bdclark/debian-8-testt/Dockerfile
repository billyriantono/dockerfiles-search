FROM bcbcarl/archlinux
MAINTAINER Carl X. Su <bcbcarl@gmail.com>

RUN \
  pacman --noconfirm -S python2-pip && \
  yes | pacman -Scc && \
  pip2 install robotframework