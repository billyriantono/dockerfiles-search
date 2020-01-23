FROM base/archlinux:latest

#Basic package needed
RUN pacman -Syyuu curl openssh git tar gzip --noconfirm --needed

#GO Installation
RUN pacman -Suu go go-tools --noconfirm --needed
RUN export GOPATH=~/go && mkdir -p $GOPATH/{bin,src} && export PATH="$PATH:$GOPATH/bin"


