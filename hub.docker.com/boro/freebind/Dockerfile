FROM ubuntu:16.04

RUN apt-get update &&  apt-get -y install curl htop make gcc libnetfilter-queue-dev git net-tools wget

RUN mkdir /home/freebind-source
RUN git clone https://github.com/blechschmidt/freebind.git /home/freebind-source/.
RUN cd /home/freebind-source &&  make install