FROM debian:stretch-slim

MAINTAINER Yves Vindevogel (yves.vindevogel@asynchrone.com)

ENV SHELL=/bin/bash

ARG DEBIAN_FRONTEND=noninteractive
ARG TIMEZONE="Europe/Brussels"

COPY ./bashrc /root/.bashrc

RUN set -x && \ 
    apt-get update --yes && \ 
    apt-get upgrade --yes && \ 
    apt-get install apt-utils --yes --no-install-recommends && \ 
    echo $TIMEZONE > /etc/timezone && \ 
    apt-get autoremove --yes && \ 
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD [ "/bin/bash" ]
