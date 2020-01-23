FROM ubuntu:bionic
MAINTAINER Simon Eames <simon.richard.eames+docker@gmail.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

# Set mirrors to AU
RUN sed -i "s/http\/\/archive./http:\/\/au.archive./g" /etc/apt/sources.list

# Install Python Runtime
RUN apt-get update && \
    apt-get install curl sudo -y && \
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - && \
    apt-get install -y nodejs

COPY . /app
WORKDIR /app

# Install application dependancies
RUN npm install -g mocha && \
    npm install

# Set mocha test runner as entrypoint
ENTRYPOINT ["mocha"]
