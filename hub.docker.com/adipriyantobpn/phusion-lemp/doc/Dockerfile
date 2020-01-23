FROM golang:latest

LABEL Aleksandar Krsteski "krsteski_aleksandar@hotmail.com"

ENV LANG=C.UTF-8

RUN apt-get update -qq  && \
    apt-get upgrade -yqq && \
#    apt-get install tmux -yqq && \
    apt-get autoremove -y

ARG user=acika
ARG uid=1000
ARG gid=1000

RUN groupadd -g $gid $user; exit 0  # do not crash on already existing GID
RUN useradd -ms /bin/bash -u $uid -g $gid $user

USER $user

WORKDIR /go
