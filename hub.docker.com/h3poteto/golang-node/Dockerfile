FROM h3poteto/golang:1.9.4

USER root

ENV NODE_VERSION 8.9.3-r0

RUN set -x \
    && apk add --no-cache \
    nodejs=${NODE_VERSION} \
    nodejs-npm=${NODE_VERSION} \
    curl

USER go
