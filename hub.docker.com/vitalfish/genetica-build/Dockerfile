FROM ubuntu:18.04

LABEL maintainer="michael.cramer@vitalfish.co"

# Env variables
ENV SCALA_VERSION 2.12.8
ENV SBT_VERSION 1.3.0

RUN apt-get update && apt-get -y install \
    gnupg2 \
    git \
    openjdk-11-jdk \
    curl \
    sed \
    unzip \
    && rm -rf /var/lib/apt/lists/*

# Set environment variables
ENV JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"

# Install sbt and scala
RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
RUN apt-get update -y
RUN apt-get install -y sbt scala

RUN mkdir -p /home/build

