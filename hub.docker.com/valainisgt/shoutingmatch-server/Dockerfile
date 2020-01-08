FROM node:8-alpine

WORKDIR /shoutingmatch-server

COPY ./src/server/package*.json ./

RUN npm install

# Bundle app source
COPY ./src/server/ .

# test
RUN npm run test

# Publish
RUN npm run build
RUN npm ci