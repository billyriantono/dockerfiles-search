FROM ubuntu:16.04

MAINTAINER Ivan Subotic "ivan.subotic@unibas.ch"

# Set timezone
#ENV TZ=ETC/GMT+1
#RUN \
#  ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
#  date

# Silence debconf messages
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# Install apt https transport needed for bintray needed for sbt.
RUN \
  apt-get update && apt-get -y install apt-transport-https && \
  echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823

RUN \
  apt-get update && apt-get -y install \
  git \
  openjdk-8-jdk \
  sbt \
  sed \
  unzip \
  && rm -rf /var/lib/apt/lists/*

# Set environment variables
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"