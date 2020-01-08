FROM openjdk:8-jre-alpine
LABEL maintainer="aikaiqiang <akqdream@163.com>"
LABEL description=" docker build -t openjdk"
RUN apk add --update ttf-dejavu dmidecode && rm -rf /var/cache/apk/*
COPY font/msyh.ttf /usr/share/fonts/msyh.ttf
