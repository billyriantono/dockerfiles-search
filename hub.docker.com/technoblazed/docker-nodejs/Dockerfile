FROM ubuntu:16.04

LABEL maintainer="i.will@spamthe.world"

# Set NodeJS version to be downloaded
ENV NODE_VERSION 9

# Update apt-sources.list and upgrade outdated packages
RUN apt-get update && apt-get upgrade -y

# Install curl for use with NodeJS
RUN apt-get install curl -y

# Update apt-sources.list for relevant NodeJS version
RUN curl -sL "https://deb.nodesource.com/setup_$NODE_VERSION.x" | bash -

# Install some useful tools
RUN apt-get install git htop nodejs -y

# Install global npm packages
RUN npm i -g babel-eslint eslint nodemon pm2
