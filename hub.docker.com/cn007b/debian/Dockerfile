FROM debian:jessie

MAINTAINER Vladimir Kovpak <cn007b@gmail.com>

ENV TERM xterm

RUN apt-get update --fix-missing

RUN apt-get install -y vim tree
RUN apt-get install -y git colordiff
RUN apt-get install -y curl net-tools telnet
RUN apt-get install -y unzip
RUN apt-get install -y libpcre3-dev
RUN apt-get install -y make
RUN apt-get install -y lsb-release

# ApacheBench
RUN apt-get install -y apache2-utils

# @TODO: Need to install ZeroMQ.
