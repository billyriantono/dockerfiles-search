FROM debian:latest
MAINTAINER Dokla Enterprise

RUN apt-get update && apt-get install -y \
    vim vim-nox vim-pathogen vim-airline-themes vim-fugitive\
    screen tree wget curl git \
    python-pip fonts-powerline

RUN pip install git+git://github.com/Lokaltog/powerline

ADD .vimrc /root/.vimrc

WORKDIR /root
