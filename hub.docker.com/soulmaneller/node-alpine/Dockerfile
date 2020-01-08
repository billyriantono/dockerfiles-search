FROM alpine:3.8
MAINTAINER oxoox22@gmail.com <Oxoox Soulmaneller>

RUN apk update \
    && apk upgrade \
    && apk add --update nodejs npm \
    && npm i -g npm \
        forever \
        supervisor \
        nodemon \
    && rm -rf /var/cache/apk/*

EXPOSE 3000
WORKDIR /app
# CMD forever forever/forever.json
CMD node index.js
