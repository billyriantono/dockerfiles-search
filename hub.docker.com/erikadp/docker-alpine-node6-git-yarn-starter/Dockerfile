FROM node:6-alpine

RUN echo -e 'http://dl-cdn.alpinelinux.org/alpine/edge/main\nhttp://dl-cdn.alpinelinux.org/alpine/edge/community\nhttp://dl-cdn.alpinelinux.org/alpine/edge/testing' > /etc/apk/repositories \
    && apk update \
    && apk add --no-cache yarn \
    && apk add git \
    && yarn global add grunt-cli \
    && yarn global add gulp

