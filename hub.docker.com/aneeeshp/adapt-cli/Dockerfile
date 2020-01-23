# Download base image ubuntu latest
FROM ubuntu:latest

# Install git & curl
RUN apt-get update -y && apt-get install git curl -y

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get update -y && apt-get install nodejs -y

# Install grunt & adapt-cli
RUN npm install -g grunt-cli adapt-cli