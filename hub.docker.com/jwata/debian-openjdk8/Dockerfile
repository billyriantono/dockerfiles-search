FROM debian:jessie-backports

MAINTAINER Junji Watanabe

RUN \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y openjdk-8-jdk

# print version
RUN java -version
