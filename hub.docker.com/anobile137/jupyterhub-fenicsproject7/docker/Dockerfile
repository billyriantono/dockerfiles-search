FROM ubuntu:18.04
MAINTAINER Andres Espindola <andres.espindolac@gmail.com>
LABEL version="1.0" description="This dockerfile is for diamond"

RUN apt-get update
RUN apt-get upgrade
RUN apt-get install -y wget
RUN mkdir -p /home/bin  && cd /home/bin
RUN wget -P /home/bin/ https://github.com/bbuchfink/diamond/releases/download/v0.9.22/diamond-linux64.tar.gz
RUN tar xzf /home/bin/diamond-linux64.tar.gz -C /home/bin

ENV PATH=/home/bin:$PATH
CMD which diamond -h