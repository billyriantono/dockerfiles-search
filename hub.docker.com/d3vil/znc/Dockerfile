FROM debian:jessie

MAINTAINER Ilya <d3vil.st@gmail.com> Kargapolov

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get dist-upgrade -y
RUN echo 'deb http://httpredir.debian.org/debian stretch main' >> /etc/apt/sources.list
RUN apt-get update && apt-get install -y znc
RUN adduser -q --disabled-password --gecos "" znc
RUN chown -R znc:znc /home/znc
USER znc
WORKDIR /home/znc
CMD znc -f
