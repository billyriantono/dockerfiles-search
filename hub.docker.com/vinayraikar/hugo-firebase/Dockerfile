FROM node:9.8.0-alpine

# labels
LABEL maintainer="rockraikar@gmail.com"

# variables
ENV HUGO_VERSION 0.37.1

# install hugo
RUN set -x && \
  apk add --no-cache wget ca-certificates git && \
  update-ca-certificates && \
  cd /tmp &&\
  wget https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz -O hugo.tar.gz && \
  tar xzf hugo.tar.gz && \
  mv hugo /usr/bin/hugo && \
  rm -r * && \
  apk del wget

# install firebase-cli
RUN npm install -g firebase-tools
