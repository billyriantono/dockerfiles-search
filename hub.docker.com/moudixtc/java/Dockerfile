FROM ubuntu:16.04

LABEL maintainer="Di Mou <moudi717@gmail.com>" \
      image="moudixtc/java:8"

RUN apt-get update && \
    apt-get install -y locales && \
    locale-gen en_US.UTF-8

ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0x219BD9C9 && \
    echo "deb http://repos.azulsystems.com/ubuntu stable main" >> /etc/apt/sources.list.d/zulu.list

ARG java_major_version=8
RUN apt-get update && \
    apt-get install -y zulu-${java_major_version}

ENV JAVA_HOME=/usr/lib/jvm/zulu-${java_major_version}-amd64/bin/java
