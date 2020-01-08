# Use Ubuntu 12.04 as the base image
FROM ubuntu:12.04

MAINTAINER Akihiro Sei "https://github.com/akisei"
 
# Install a bunch of prerequisites
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list && \
        apt-get update && \
        apt-get upgrade
RUN apt-get install -y git-core curl wget python-yaml build-essential libssl-dev

# Ensure UTF-8
RUN locale-gen en_US.UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

# Install ruby-build
RUN git clone https://github.com/sstephenson/ruby-build.git
RUN cd ruby-build && ./install.sh
RUN mkdir -p /opt/rubies
 
# Install Ruby 2.0.0-p353
RUN /usr/local/bin/ruby-build 2.0.0-p353 /opt/rubies/2.0.0-p353
ENV PATH /app/bin:/app/vendor/bundle/bin:/opt/rubies/2.0.0-p353/bin:/usr/local/bin:/usr/bin:/bin
RUN gem install bundler
