FROM alpine:3.9

RUN apk add --update postgresql-client coreutils\
    && rm -rf /var/cache/apk/*

LABEL maintainer="attila@attilanagy.net"
LABEL Description="Alpine based Python image contains PostgreSQL client"
