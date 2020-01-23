FROM ubuntu:18.04

MAINTAINER Jordi Rejas <dockerhub@rejas.eu>

RUN apt-get update && apt-get install -y curl

# NODEJS
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt-get install -y nodejs

# YARN
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
apt-get update && apt-get install yarn -y

RUN mkdir /var/project

WORKDIR /var/project