FROM node:9.9-alpine

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies & build tools & cleanup (keep a light layer)
RUN apk add --no-cache git make gcc g++ python && \
  git clone git://github.com/bcoin-org/bcoin.git && \
  cd bcoin && \
  npm install --silent --production && \
  apk del git make gcc g++ python

WORKDIR /usr/src/app/bcoin
