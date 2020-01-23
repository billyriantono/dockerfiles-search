FROM debian:jessie-slim

MAINTAINER Gareth Price <gareth@capen.co.uk>

# Clean, update & upgrade
RUN apt-get update && \
    apt-get install -y --no-install-recommends git zip unzip nano && \
    apt-get clean && \
    apt-get install -y curl ssh

## Install NodeJS - this installs the correct version
RUN curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh && \
    bash nodesource_setup.sh

RUN apt-get install -y nodejs && \
    npm install -g gulp bower polymer-cli generator-polymer-init-custom-build

## Setup some aliases
RUN touch /root/.bashrc && \
    echo "alias dir='ls -alh'" >> /root/.bashrc && \
    echo "alias pico='nano -c'" >> /root/.bashrc && \
    echo "alias bower='bower --allow-root'" >> /root/.bashrc