FROM ubuntu:16.04

# Update package repos

RUN apt-get update && apt-get install -y software-properties-common python-software-properties apt-transport-https

# Install Java

RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
RUN apt-get install -y oracle-java8-installer
RUN apt-get install -y oracle-java8-set-default

# Install Node

RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

# Install nginx and LetsEncrypt Certbot

RUN add-apt-repository ppa:certbot/certbot
RUN apt-get update
RUN apt-get install -y nginx python-certbot-nginx
