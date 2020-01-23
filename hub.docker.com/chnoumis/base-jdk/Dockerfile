FROM chnoumis/base-sti:2.0.0

MAINTAINER chnoumis

USER root

RUN \
  apk update && \
  apk upgrade && \
  apk add openjdk7-jre && \
  rm -rf /var/cache/apk/*
 
 ENV JAVA_HOME /usr/lib/jvm/java-1.7-openjdk 
  
USER chnoumis