FROM alpine:3.4

MAINTAINER docker@scispike.com

RUN \
  set -x \
  && \
  apk add --no-cache \
    bash \
    g++ \
    git \
    make \
    nodejs-lts \
    python \
    sudo \
    sed

RUN adduser -D -u 1000 node
RUN echo "node ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER node
RUN echo 'export PATH="./node_modules/.bin:$PATH"' >> ~/.profile

USER root
RUN echo 'export PATH="./node_modules/.bin:$PATH"' >> ~/.profile
