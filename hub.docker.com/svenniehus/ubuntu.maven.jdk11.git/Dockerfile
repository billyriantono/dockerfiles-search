FROM ubuntu:rolling
MAINTAINER Sven Niehus <sven@niehus.eu>

# apt update
RUN apt-get update

# Set the locale
RUN apt-get install -y locales 
RUN rm -rf /var/lib/apt-get/lists/*
RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

# Install git
RUN apt-get install -y git

# Install maven
RUN apt-get install -y maven

# Install jdk 11
RUN apt-get install -y openjdk-11-jdk
