FROM shurshun/alpine-moscow

LABEL author "Korviakov Andrey"
LABEL maintainer "4lifenet@gmail.com"

ARG LSYNCD_REPO="https://github.com/shurshun/lsyncd"

RUN \
    apk add --no-cache --update --virtual .build-deps \
        build-base \
        patch \
        cmake \
        make \
        git \
        lua-dev \
    \
    && apk add --no-cache --update lua \
    \
    && git clone $LSYNCD_REPO /tmp/lsyncd \
    && cd /tmp/lsyncd \
    && patch < alpine/fix-realpath.patch \
    && cmake . \
    && make \
    && cp lsyncd /usr/bin/ \
    \
    && cd / \
    && rm -rf /tmp/* \
    && apk del .build-deps
