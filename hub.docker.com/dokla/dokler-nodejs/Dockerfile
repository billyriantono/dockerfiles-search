FROM dokla/dokler-vim:latest

MAINTAINER Dokla Enterprise

RUN apt-get update && apt-get install -y \
    curl software-properties-common

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

RUN apt-get install -y nodejs
    

WORKDIR /root
