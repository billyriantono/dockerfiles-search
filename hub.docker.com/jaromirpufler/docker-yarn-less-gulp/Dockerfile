FROM node:10.9-alpine

RUN apk add --no-cache git docker yarn && \
    npm install -g gulp-cli less && \
    mkdir -p /.config && \
    chmod 777 /.config && \
    mkdir -p /.local && \
    chmod 777 /.local && \
    mkdir -p /.cache && \
    chmod 777 /.cache && \
    mkdir -p /.npm && \
    chmod 777 /.npm
WORKDIR /data
