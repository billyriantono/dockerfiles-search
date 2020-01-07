FROM eltiempoes/centos7-cli-tools:latest
ENV REFRESHED_AT 2018-03-28
LABEL maintainer "it@eltiempo.es"
LABEL version "1.0"
LABEL description "Image with some cli tools for dev environment and Phalcon Framework"
ENV container docker

USER root
RUN yum -y --setopt=tsflags=nodocs install gcc libtool pcre-devel git php71w-devel re2c file make

RUN git clone --depth=1 "git://github.com/phalcon/cphalcon.git" && \
    cd cphalcon/build && \
    ./install

COPY phalcon.ini /etc/php.d

USER cli-user
WORKDIR /home/cli-user