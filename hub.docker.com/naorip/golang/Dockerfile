FROM golang:1.13-alpine
# Dockerfile内でonにしないと、Dockerfileのビルド時にこける
WORKDIR /go/bin/app

# apk
RUN set -eux && \
  apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  apk del .build-dependencies

RUN apk add --no-cache \
        git \
        curl \
        jq
