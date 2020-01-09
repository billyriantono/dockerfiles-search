FROM ubuntu:16.04

MAINTAINER FUJIMOTO Satoshi

USER root
WORKDIR /root

RUN apt-get update && apt-get upgrade -y \
 && apt-get install wget gcc make libjson-c-dev libreadline6 libreadline6-dev texinfo telnet -y \
 && wget https://github.com/FRRouting/frr/releases/download/frr-2.0/frr-2.0.tar.gz \
 && tar xvf frr-2.0.tar.gz \
 && cd frr-2.0 \
 && ./configure && make && make install \
 && echo include /usr/local/lib >> /etc/ld.so.conf \
 && ldconfig \
 && mv /usr/local/etc/bgpd.conf.sample /usr/local/etc/bgpd.conf

