FROM node:9.2.0-alpine

RUN apk add --no-cache \
    git openssh openjdk8-jre

RUN yarn global add npm-cli-login

COPY assets /usr/local/bin
