FROM ubuntu:14.04

MAINTAINER Innovativos SA <opensource@innovativos.com.gt>

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y locales
RUN apt-get clean

RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales && \
    locale-gen es_GT.UTF-8 && \
    /usr/sbin/update-locale LANG=es_GT.UTF-8

ENV LC_ALL es_GT.UTF-8
ENV LANGUAGE es_GT.UTF-8
ENV LANG es_GT.UTF-8

