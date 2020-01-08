FROM ubuntu:16.04

# Update packages lists.
RUN apt-get update -y && \
    apt-get upgrade -y

# Install curl to pull the nodejs install script.
RUN apt-get install curl -y

# Install Node.js 10
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs

# Install ReactJS
RUN npm install -g create-react-app