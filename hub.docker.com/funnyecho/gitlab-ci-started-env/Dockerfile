FROM node:10-alpine

# https://github.com/nodejs/docker-node/blob/master/docs/BestPractices.md#global-npm-dependencies
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global
ENV PATH=$PATH:/home/node/.npm-global/bin

USER root

RUN apk update && apk upgrade && \
    apk add --no-cache git

USER node

RUN npm install -g tslint typescript && \
    npm install -g gulp-cli