FROM ubuntu:14.04

MAINTAINER Sergei Olshanetski <sergei@tikalk.com>

#install sbt
RUN echo "deb http://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list \
        && sudo apt-get update \
        && sudo apt-get install -y --force-yes sbt

RUN apt-get install -y wget vim curl
RUN apt-get install -y openjdk-7-jdk
