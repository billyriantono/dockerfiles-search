FROM node:10.15.3-alpine
LABEL maintainer="Angga Lanuma <lanuma.angga@gmail.com>"

RUN apk add --no-cache git openssh nodejs npm bash curl rsync \
    && npm install pm2@latest -g

WORKDIR /app


