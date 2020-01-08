FROM ubuntu:trusty

# shut up debconf messages (https://github.com/phusion/baseimage-docker/issues/58)
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

# Needed for add-apt-repository, curl
RUN apt-get -y install software-properties-common curl

# Install Java.
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

