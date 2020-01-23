FROM alpine:3.7
MAINTAINER Stephan Deglow <info@deglowdesign.de>

# Install packages needed to build
RUN apk add --update --no-cache \
    bash \
    ncftp \
    ca-certificates \
    curl \
    wget \
    openssh-client &&\
    rm -rf /var/cache/apk/*

# Install hugo.
ARG HUGO_VERSION=0.58.3
ARG HUGO_SHA256=92aeeb64d4c392782cb55424dc2cc594a06ad5e1bc7e156480feab488ff7e774

# Rember sha256sum (and md5sum) expect 2 spaces in front of the filename on alpine...
RUN curl -Ls https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz \
       -o /tmp/hugo.tar.gz \
  && echo "${HUGO_SHA256}  /tmp/hugo.tar.gz" | sha256sum -c - \
  && tar xf /tmp/hugo.tar.gz -C /tmp \
  && mv /tmp/hugo /usr/bin/hugo \
  && rm -rf /tmp/hugo* \
