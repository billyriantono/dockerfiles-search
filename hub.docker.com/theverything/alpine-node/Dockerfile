FROM alpine:3.4

ENV NODE_VERSION=6.6.0-r0

RUN apk add --no-cache make gcc g++ python && \
    apk add nodejs=$NODE_VERSION --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/main
