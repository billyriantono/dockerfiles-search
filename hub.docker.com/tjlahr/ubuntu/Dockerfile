FROM ubuntu:14.04
MAINTAINER Thomas Lahr <tjlahr@gmail.com>

RUN apt-get update && apt-get install -y -q \
  curl \
  git \
  maven \
  default-jre \
  default-jdk

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64/jre
