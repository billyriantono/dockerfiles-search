FROM node:11.10.0-alpine

MAINTAINER Anthony Smith <anthony@sticksnleaves.com>

ENV APP_HOME /usr/src/app

RUN apk add --no-cache --virtual .build-deps curl && \
    apk add --no-cache --virtual .build-deps gnupg

RUN curl -L https://github.com/npm/cli/archive/latest.tar.gz -o npm.tar.gz && \
    tar xzf npm.tar.gz && \
    cli-latest/scripts/install.sh && \
    rm -f npm.tar.gz && \
    rm -rf cli-latest

RUN curl -o- -L https://yarnpkg.com/install.sh | ash

RUN apk del .build-deps

WORKDIR $APP_HOME

COPY docker-entrypoint.sh /usr/local/bin

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
