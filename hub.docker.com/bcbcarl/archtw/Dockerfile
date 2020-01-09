FROM bcbcarl/archlinux
MAINTAINER Carl X. Su <bcbcarl@gmail.com>

RUN \
  ln -s /usr/share/zoneinfo/Asia/Taipei /etc/localtime && \
  sed -i -e '1i'$'Server = http://ftp.tku.edu.tw/Linux/Archlinux/$repo/os/$arch' /etc/pacman.d/mirrorlist && \
  sed -i -e '1i'$'Server = http://archlinux.cs.nctu.edu.tw/$repo/os/$arch' /etc/pacman.d/mirrorlist && \
  sed -i -e 's|^#zh_TW.UTF-8|zh_TW.UTF-8|' /etc/locale.gen && \
  locale-gen

ENV LC_ALL zh_TW.UTF-8