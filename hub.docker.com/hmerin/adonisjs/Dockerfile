FROM node:8.11-alpine

WORKDIR /usr/src/app

RUN set -e \
    && apk update \
    && apk add --no-cache \
        wget \
        ca-certificates \
        sed \
    && npm i -g @adonisjs/cli \
    && rm -rf /var/cache/apk/*

EXPOSE 3333

COPY entrypoint.sh /usr/local/bin/

ENTRYPOINT [ "entrypoint.sh" ]