FROM node:8.10-alpine

ENV NODE_ENV=development

RUN apk update \
  && apk upgrade \
  && apk add --no-cache \
    git \
    make \
    gcc \
    g++ \
    python \
    bash \
    openssh

RUN npm config set unsafe-perm true

WORKDIR /bitcore

COPY package.json ./
COPY lerna.json ./
RUN npm install

COPY ./packages/bitcore-build/package.json ./packages/bitcore-build/
COPY ./packages/bitcore-client/package.json ./packages/bitcore-client/
COPY ./packages/bitcore-lib/package.json ./packages/bitcore-lib/
COPY ./packages/bitcore-lib-cash/package.json ./packages/bitcore-lib-cash/
COPY ./packages/bitcore-mnemonic/package.json ./packages/bitcore-mnemonic/
COPY ./packages/bitcore-node/package.json ./packages/bitcore-node/
COPY ./packages/bitcore-p2p/package.json ./packages/bitcore-p2p/
COPY ./packages/bitcore-p2p-cash/package.json ./packages/bitcore-p2p-cash/
COPY ./packages/bitcore-payment-protocol/package.json ./packages/bitcore-payment-protocol/
COPY ./packages/bitcore-wallet/package.json ./packages/bitcore-wallet/
COPY ./packages/bitcore-wallet-client/package.json ./packages/bitcore-wallet-client/
COPY ./packages/bitcore-wallet-service/package.json ./packages/bitcore-wallet-service/

#COPY ./packages/bitcore-wallet-ui/package.json ./packages/bitcore-wallet-ui/
#COPY ./packages/insight/package.json ./packages/insight/
#COPY ./packages/insight-previous/package.json ./packages/insight-previous/

RUN npm cache verify
RUN npm run bootstrap

RUN apk del \
  git \
  make \
  gcc \
  g++

RUN rm /var/cache/apk/*

COPY . .

RUN npm run compile
