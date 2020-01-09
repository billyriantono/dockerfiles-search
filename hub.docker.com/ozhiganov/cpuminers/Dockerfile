FROM ubuntu:16.04
MAINTAINER Evgeniy N. Ozhiganov <eozhiganov@ya.ru>

RUN apt-get autoclean && apt-get autoremove && apt-get update && apt-get -qqy install git
RUN git clone https://github.com/Ozhiganov/cpuminers

WORKDIR /cpuminers
