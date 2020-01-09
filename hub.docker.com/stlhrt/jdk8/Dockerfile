FROM ubuntu:14.04.1
MAINTAINER Łukasz Woźniak

RUN apt-get update
RUN apt-get install python-software-properties software-properties-common curl libssl-dev man -y --no-install-recommends

# Install Java
ADD install-java.sh /tmp/install-java.sh
RUN /tmp/install-java.sh

RUN useradd -m service

RUN mkdir -p /app/service
RUN mkdir -p /app/logs
RUN mkdir -p /app/data

RUN chown -R service:service /app

# Cleanup unnecessary files
RUN apt-get -qq clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/oracle-jdk8-installer

USER service
WORKDIR /app/service

VOLUME /app/logs
VOLUME /app/data
ENV JAVA_HOME /usr/local/java
ENV PATH $PATH:${JAVA_HOME}/bin
ENV HOME /home/service
