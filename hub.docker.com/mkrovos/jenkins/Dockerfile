FROM cypress/base:8

MAINTAINER mkr@ovos.at

RUN set -ex && \
    echo 'deb http://deb.debian.org/debian jessie-backports main' \
      > /etc/apt/sources.list.d/jessie-backports.list && \
    apt-get update -y && \
    apt-get install -y -t \
      jessie-backports \
      openjdk-8-jre-headless \
      ca-certificates-java
