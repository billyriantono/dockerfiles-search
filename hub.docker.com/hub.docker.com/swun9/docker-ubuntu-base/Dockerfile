FROM ubuntu:14.04
MAINTAINER swun9 "swung.cn@gmail.com"
ENV REFRESHED_AT 2015-01-11

RUN \
  sed -i 's/archive.ubuntu.com/mirrors.163.com/g' /etc/apt/sources.list && \
  apt-get -qq update

RUN \
  apt-get -qqy install build-essential && \
  apt-get -qqy install software-properties-common && \
  apt-get -qqy install curl wget vim tree byobu git unzip && \
  rm -rf /var/lib/apt/lists/*

ADD root/bashrc /root/.bashrc
ADD root/gitconfig /root/.gitconfig
ADD root/scripts /root/.scripts

ENV HOME /root

WORKDIR /root

CMD ["bash"]
