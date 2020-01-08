FROM alpine:3.10

LABEL maintainer="Tom Winterhalder <tom.winterhalder@gmail.com>"

RUN apk add --no-cache tzdata curl ca-certificates openssl && \
    update-ca-certificates && \
    cp /usr/share/zoneinfo/Europe/Zurich /etc/localtime && \
    echo "Europe/Zurich" > /etc/timezone && \
    addgroup -g 1000 basegroup && \
    adduser -u 1000 -G basegroup -D baseuser && \
    rm -f /var/cache/dpk/*
