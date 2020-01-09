FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list
RUN apt-get update -y
RUN apt-get install -y aptitude curl wget debian-keyring debian-archive-keyring apt-transport-https vim

RUN mkdir /logs /cache /data

VOLUME /logs
VOLUME /cache
VOLUME /data
