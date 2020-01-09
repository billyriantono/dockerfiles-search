# Base image to tag trebomat/gfp-node-base
FROM node:10.8.0-alpine
MAINTAINER Mathieu Obert <trebomat@gmail.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

# Install Python 2.7 (for sharp)
RUN apk add --no-cache python && \
    python -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip install --upgrade pip setuptools && \
    rm -r /root/.cache && \
# Update vips (for sharp)
    apk add --update \
       --repository http://dl-3.alpinelinux.org/alpine/edge/testing \
       vips-tools vips-dev fftw-dev gcc g++ make libc6-compat && \
    rm -rf /var/cache/apk/* && \
# Add a user "myuser" to avoid running as root
    adduser -S myuser && \
# Fix PhantomJS
    echo "Fixing PhantomJS" && \
    apk add --update git build-base curl bash && \
    curl -Ls "https://github.com/dustinblackman/phantomized/releases/download/2.1.1/dockerized-phantomjs.tar.gz" | tar xz -C /

LABEL application=gofitnessplan
