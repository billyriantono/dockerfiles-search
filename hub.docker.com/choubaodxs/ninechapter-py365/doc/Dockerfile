FROM alpine:3.3

MAINTAINER chnoumis

# User root user to install software
USER root

# Install packages
RUN apk update && apk add \
  bash \ 
  ruby \
  wget \
  curl \
  tar \
  unzip

# Add user
RUN addgroup chnoumis && adduser -s /bin/bash -D -G chnoumis chnoumis

# Create and set the working directory
RUN mkdir -p /opt/chnoumis
WORKDIR /opt/chnoumis

USER chnoumis
