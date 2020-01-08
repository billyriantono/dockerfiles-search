FROM node:alpine

MAINTAINER Greg Ninforge

WORKDIR /usr/src/node-red

RUN mkdir -p /usr/src/node-red && \
    mkdir /data && \
    apk --no-cache --update add --virtual deps curl && \
    curl -O https://raw.githubusercontent.com/node-red/node-red-docker/master/package.json && \
    apk del deps && \
    npm install

EXPOSE 1880

ENV FLOWS=flows.json

CMD ["npm", "start", "--", "--userDir", "/data"]
