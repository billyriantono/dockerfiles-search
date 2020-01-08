FROM node:9.5.0
MAINTAINER Nicolas Brugneaux <nicolas.brugneaux@gmail.com>

RUN mv /usr/local/lib/node_modules/npm /tmp/.npm && \
  node /tmp/.npm/bin/npm-cli.js i -g npm@latest && \
  rm -rf /tmp/.npm

ENV NPM_CONFIG_LOGLEVEL "warn"

