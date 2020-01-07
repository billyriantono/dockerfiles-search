FROM ubuntu:xenial
LABEL maintainer="Tiryoh <tiryoh@gmail.com>"

RUN apt-get update -q && \
    apt-get install -yq software-properties-common &&\
    apt-add-repository ppa:jonathonf/vim && \
    apt-get update -q && \
    apt-get upgrade -yq && \
    apt-get install -yq wget curl git build-essential vim sudo lsb-release locales bash-completion && \
    rm -rf /var/lib/apt/lists/*
RUN useradd -m -d /home/ubuntu ubuntu -p `perl -e 'print crypt("ubuntu", "salt"),"\n"'` && \
    echo "ubuntu ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN locale-gen en_US.UTF-8
USER ubuntu
WORKDIR /home/ubuntu
ENV HOME=/home/ubuntu
ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8
RUN git clone https://github.com/Tiryoh/oneliners.git && \
    git clone https://github.com/Tiryoh/dotfiles.git && \
    /bin/bash -c 'cd ${HOME}/dotfiles; make vim; make deinvim; ./etc/docker/vim_setup.sh; make bash'
