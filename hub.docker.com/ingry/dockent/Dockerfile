FROM debian:stable
MAINTAINER Stepan Koci <stepan.koci@gmail.com>

ENV TERM xterm
ENV HOME /root
ENV TAG stable

COPY sources.list  /resources/debian/sources.list
COPY install.sh    /resources/debian/install.sh
RUN /resources/debian/install.sh

COPY . /resources/debian

WORKDIR ${HOME}

RUN /resources/debian/shared/configure-user.sh
