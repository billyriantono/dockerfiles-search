FROM node:8-alpine

MAINTAINER Igor Ilic

# Install yarn

ENV YARN_VERSION 1.2.1
ENV PATH /root/.yarn/bin:$PATH

RUN apk update \
  && apk add curl bash binutils tar \
  && rm -rf /var/cache/apk/* \
  && /bin/bash \
  && touch ~/.bashrc \
  && curl -o- -L https://yarnpkg.com/install.sh | bash \
  && apk del curl tar binutils

# Update npm

RUN npm install -g npm

