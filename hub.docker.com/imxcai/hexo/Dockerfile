FROM ubuntu:18.04
MAINTAINER imxcai <imxcai@gmail.com>
ENV REFRESHED_AT 2019-04-29

RUN apt update -yqq
RUN apt install git nodejs npm -yqq

RUN npm install -g hexo-cli
VOLUME ["/hexo"]

