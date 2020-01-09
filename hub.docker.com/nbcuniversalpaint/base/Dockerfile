FROM alpine:latest

MAINTAINER "Vaughan Jones <vaughan.jones@nbcuni.com>"

RUN addgroup -g 8080 digitalnbcu && \
    adduser -u 8080 -s /bin/false -D -G digitalnbcu digitalnbcu && \
    mkdir -pv /usr/src/app && \
    chown -R digitalnbcu:digitalnbcu /usr/src/app
