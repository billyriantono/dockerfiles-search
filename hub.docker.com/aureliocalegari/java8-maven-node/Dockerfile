FROM ubuntu:18.04

MAINTAINER Aurelio Calegari "aureliocalegari@gmail.com"

ENV NODE_VERSION 10.13.0
ENV OPEN_JDK openjdk-8-jdk

ARG DEBIAN_FRONTEND=noninteractive

# Initial distro update
RUN echo "# Updateding OS" \
    && apt-get -y update \
    && apt-get -y dist-upgrade \
    && apt-get install -y wget git curl zip monit openssh-server iptables ca-certificates daemon net-tools libfontconfig-dev sudo build-essential libjpeg-dev python3

# Install Java and maven
RUN echo "# Installing ${OPEN_JDK}" \
    && apt-get -y install ${OPEN_JDK} maven \
    && update-java-alternatives -s java-1.8.0-openjdk-amd64

RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - \
    && apt install -y nodejs

RUN apt-get install -y python3-pip

VOLUME maven-repo:/root/.m2
