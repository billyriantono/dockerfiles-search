FROM ubuntu
MAINTAINER Simon Dittlmann

RUN apt-get update && \
  apt-get install -y curl git openjdk-8-jre bzip2

RUN curl nodejs.org/dist/v0.10.45/node-v0.10.45-linux-x64.tar.gz -O && \
  tar -C /usr/local --strip-components 1 -xzf node-v0.10.45-linux-x64.tar.gz
