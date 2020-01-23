# Dockerfile for https://github.com/adnanh/webhook
FROM        golang:alpine3.7 AS build
MAINTAINER  Almir Dzinovic <almir@dzinovic.net>
WORKDIR     /go/src/github.com/adnanh/webhook
ENV         WEBHOOK_VERSION 2.6.8
RUN         apk add --update -t build-deps curl libc-dev gcc libgcc
RUN         curl -L --silent -o webhook.tar.gz https://github.com/adnanh/webhook/archive/${WEBHOOK_VERSION}.tar.gz && \
            tar -xzf webhook.tar.gz --strip 1 &&  \
            go get -d && \
            go build -o /usr/local/bin/webhook && \
            apk del --purge build-deps && \
            rm -rf /var/cache/apk/* && \
            rm -rf /go

FROM        alpine:3.7
RUN         echo -e "https://mirror.tuna.tsinghua.edu.cn/alpine/v3.4/main\n\
            https://mirror.tuna.tsinghua.edu.cn/alpine/v3.4/community" > /etc/apk/repositories
RUN         apk --update add curl bash git && \
            rm -rf /var/cache/apk/*
COPY        --from=build /usr/local/bin/webhook /usr/local/bin/webhook
EXPOSE      9000
ENTRYPOINT  ["/usr/local/bin/webhook"]
