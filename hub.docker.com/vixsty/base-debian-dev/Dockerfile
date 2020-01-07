FROM debian:jessie

MAINTAINER LARQUEMIN Kevin "kevin@oosp.fr"

ENV LANG C.UTF-8

# Installation d'outils
RUN apt-get update \
		&& apt-get install -y zsh curl wget git htop unzip software-properties-common net-tools emacs-nox sudo apt-transport-https \
		&& apt-get clean \
		&& rm -rf /var/lib/apt/lists/*

# Installation de oh-my-zsh et sélection de zsh comme shell par défault
RUN curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | zsh || true &&\
    chsh -s /bin/zsh
