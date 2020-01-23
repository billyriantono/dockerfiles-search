FROM node:8

WORKDIR /
COPY package.json package.json
COPY proxylistener.js proxylistener.js
COPY config.json config.json
RUN npm install

ENTRYPOINT node proxylistener.js
