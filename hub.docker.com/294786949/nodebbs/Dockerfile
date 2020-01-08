#
# Dockerfile for nodebb
#
FROM node:6.11.0-alpine
MAINTAINER kev <294786949@qq.com>

ENV BB_VER 1.5.1
ENV BB_URL https://github.com/NodeBB/NodeBB/archive/v$BB_VER.tar.gz
ENV BB_SOURCE /usr/src/nodebb
ENV BB_CONTENT /var/lib/nodebb

WORKDIR $BB_SOURCE
VOLUME $BB_CONTENT

RUN set -ex \
    && apk add -U bash \
                  imagemagick \
                  krb5-libs \
                  git \
                  openssl \
    && apk add -t TMP build-base \
                      curl \
                      krb5-dev \
                      openssl-dev \
                      tar \
    && curl -sSL $BB_URL | tar xz --strip 1 \
    && npm install --production \
    && npm cache clean \
    && apk del TMP \
    && rm -rf /tmp/npm* \
              /var/cache/apk/*

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 4567
CMD ["npm", "start"]
