# OpenJDK image
FROM astau/alpine:latest

MAINTAINER Srikanth <srikanth@astau.com>

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

RUN  apk add openjdk8 \
  && rm -rf /var/cache/apk/*

ENV JAVA_HOME /usr/lib/jvm/default-jvm
ENV PATH $PATH:$JAVA_HOME/bin
