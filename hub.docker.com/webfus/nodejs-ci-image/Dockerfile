FROM node:8-alpine as builder

RUN apk add --no-cache --virtual .watchman linux-headers inotify-tools openssl && \
    apk add --no-cache --virtual .watchman-build gcc g++ curl autoconf automake libtool make openssl-dev

WORKDIR /watchman

ENV WATCHMAN_VERSION 4.9.0

RUN curl -L -o watchman.tgz https://github.com/facebook/watchman/archive/v${WATCHMAN_VERSION}.tar.gz && \
    tar xf watchman.tgz && \
    cd watchman-${WATCHMAN_VERSION} && \
    ./autogen.sh && \
    ./configure --enable-statedir=/tmp --without-python && make

FROM webfus/nodejs-ci-image:8-gyp

ENV WATCHMAN_VERSION 4.9.0

COPY --from=builder /watchman/watchman-${WATCHMAN_VERSION} /watchman/watchman-${WATCHMAN_VERSION}

RUN apk add --no-cache --virtual .watchman linux-headers inotify-tools openssl && \
    apk add --no-cache --virtual .watchman-build autoconf automake libtool make openssl-dev && \
    cd /watchman/watchman-${WATCHMAN_VERSION} && make install && cd / && rm -rf /watchman && \
    apk del .watchman-build
