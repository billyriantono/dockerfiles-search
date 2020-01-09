# version: 		0.5
# git: 	   		https://github.com/therojam/archdevel-docker
# description:	dockerfile for archlinux devel - aur package testing
# docu:			archdeveldocker.github.io

FROM archlinux/base

ENV HOSTNAME="archdevel"

RUN pacman -Syu --needed --noconfirm base-devel git sudo openssh pacman-contrib vim zsh go

RUN useradd -ms /bin/zsh arch \
	&& echo "arch ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER arch
WORKDIR /home/arch

COPY .zshrc.tmp /home/arch/.zshrc

RUN git clone https://aur.archlinux.org/yay.git

RUN  cd yay && makepkg -scfi --noconfirm
