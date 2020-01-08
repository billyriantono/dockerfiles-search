FROM node:6.10.3-alpine

RUN apk --no-cache update && \
    apk --no-cache add bash \
    openssh \
    git && \
    npm install -g yarn && \
    rm -rf /var/cache/apk/*
