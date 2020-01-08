FROM debian:buster

LABEL maintainer="wimpunk@gmail.com"
LABEL version="1.3"

RUN echo "deb http://security.debian.org/ buster/updates main" >> /etc/apt/sources.list

RUN apt-get update \
    && apt-get -yqqf --no-install-recommends install \
        apt-transport-https \
        lsb-release \
        ca-certificates \
        curl \
    && apt-get clean 


RUN apt-get update \
    && apt-get -y --no-install-recommends install \
        git \
        mc \
        vim \
        bash-completion \
        groff \
        man \
        less \
    && apt-get clean

RUN apt-get -y upgrade \
    && apt-get clean

