FROM ubuntu:latest

MAINTAINER Stefan Sundkvist <docker@sundkvist.eu>

ENV DEBIAN_FRONTEND noninteractive

# Update Ubuntu
RUN apt-get update

RUN apt-get upgrade -y

RUN apt-get install -y curl lib32gcc1

# Prepare dirs and download steamcmd
RUN mkdir -p /srv/steamcmd

WORKDIR /srv/steamcmd

RUN curl -s http://media.steampowered.com/installer/steamcmd_linux.tar.gz | tar -vxz

# Create user and get ready to run steamcmd
RUN adduser steam

RUN chown -R steam .

VOLUME ['/srv/steamcmd']

ENTRYPOINT ["./steamcmd.sh"]
