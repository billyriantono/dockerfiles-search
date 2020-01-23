# build for amd64
FROM alpine:latest

# build for arm32 like [raspberry pi] or [tinker board]
#FROM arm32v6/alpine:latest

MAINTAINER tian <t@hitian.info>

# for chinese user
#RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

RUN apk update && apk add --no-cache build-base git texinfo && \
    git clone https://github.com/jech/polipo /tmp/polipo && \
    cd /tmp/polipo && make all && make install && mkdir -p /etc/polipo && \
    cp /tmp/polipo/config.sample /etc/polipo/config && \
    rm -rf /tmp/polipo && apk del build-base git texinfo