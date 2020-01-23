FROM hrektts/ubuntu:latest
MAINTAINER mps299792458@gmail.com

RUN apt-get update \
 && apt-get install -y curl emacs24-nox emacs24-el emacs24-common-non-dfsg \
      git htop screen tcpdump tree zsh \
 && adduser --disabled-login --gecos 'Developper' dev \
 && passwd -d dev \
 && gpasswd -a dev sudo \
 && chsh -s /usr/bin/zsh dev \
 && rm -rf /var/lib/apt/lists/*

USER dev
WORKDIR /home/dev
ENV HOME /home/dev
ENV TERM xterm

RUN git clone https://github.com/seebi/dircolors-solarized.git \
 && ln -sf dircolors-solarized/dircolors.ansi-universal .dircolors \
 && git clone https://github.com/hrektts/dotfiles.git \
 && ln -sb dotfiles/.screenrc . \
 && ln -sb dotfiles/.zshenv . \
 && ln -sf dotfiles/.zsh.d . \
 && ln -sf dotfiles/.emacs.d .

VOLUME ["/home/dev/ws"]
