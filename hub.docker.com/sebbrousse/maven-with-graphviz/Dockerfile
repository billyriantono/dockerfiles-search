FROM maven:3.5-jdk-8

MAINTAINER Sébastien Brousse <seb.brousse@gmail.com>

RUN apt-get update \
 && apt-get install -y --no-install-recommends graphviz \
 && apt -y autoremove \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

