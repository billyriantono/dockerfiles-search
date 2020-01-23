FROM ubuntu:16.04

MAINTAINER Augustus Wang <wangdw.augustus@gmail.com>

RUN apt-get update;
RUN apt-get -y upgrade

RUN apt-get -y install vim git lsb-release sudo curl

COPY ./ /clusterfuzz
WORKDIR clusterfuzz
RUN ./local/install_deps.bash

