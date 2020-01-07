FROM nginx:1.13.8-alpine

MAINTAINER UPX Technologies "labs@upx.com"

RUN apk add --update --no-cache \
    --repository http://dl-cdn.alpinelinux.org/alpine/v3.7/main/ nodejs=8.9.3-r1

RUN mkdir -p /app

WORKDIR /app

COPY nginx.conf /etc/nginx/nginx.conf
