FROM ubuntu:16.04

MAINTAINER Reto Hasler <reto.hasler@asciich.ch>

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

RUN echo "Europe/Zurich" > /etc/timezone && \
    apt-get update && \
    apt-get install -y\
        pdftk \
        vim \
    &&\
    apt-get clean