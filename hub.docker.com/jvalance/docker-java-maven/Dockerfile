#
# Ubuntu with Java and Maven

# pull base image
FROM ubuntu:latest
MAINTAINER Jeremy Valance "jvalance@blackducksoftware.com"

RUN \
  apt-get update && \
  apt-get install -y openjdk-8-jdk && \
  apt-get install -y maven && \
  apt-get install -y curl && \
  rm -rf /var/lib/apt/lists/*

WORKDIR /

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64




