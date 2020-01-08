FROM python

MAINTAINER Asaad Najjar <rajjix.dev.1992@hotmail.com>

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y apt-utils
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install vim bash-completion

ENV HOME /root
RUN env

COPY .bashrc /root/

