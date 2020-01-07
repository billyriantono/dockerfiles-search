FROM node:4.8.4-alpine
MAINTAINER David Lemaitre

ENV GULP_VERSION 3.9.1
ENV BOWER_VERSION 1.8.0

ENV NPM_CONFIG_LOGLEVEL warn

# Install git as some bower packages require it
RUN apk add --no-cache \
    git

# Install Node packages
RUN npm install -g \
    gulp@"$GULP_VERSION" \
    bower@"$BOWER_VERSION"

# Allow running bower as root
RUN echo '{ "allow_root": true }' > /root/.bowerrc

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
