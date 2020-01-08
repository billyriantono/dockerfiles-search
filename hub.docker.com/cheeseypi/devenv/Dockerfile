FROM ubuntu:18.04

RUN apt update && apt -y upgrade
RUN apt install -y vim git python python3.6

RUN git clone https://github.com/cheeseypi/dotfiles ~/.dotfiles
RUN rm ~/.bashrc
RUN ~/.dotfiles/install

RUN git clone https://github.com/VundleVim/Vundle.vim ~/.vim

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs npm
