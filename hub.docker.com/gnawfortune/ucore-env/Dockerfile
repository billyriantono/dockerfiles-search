FROM dorowu/ubuntu-desktop-lxde-vnc

RUN apt-get update \
  && sudo apt-get -y upgrade \
  && sudo apt-get -y install build-essential git qemu-system-x86 vim-gnome gdb cgdb eclipse-cdt \
  make diffutils exuberant-ctags tmux openssh-server cscope meld qgit gitg gcc-multilib gcc-multilib g++-multilib

ADD ./ucore_os_lab.tar.gz /root/