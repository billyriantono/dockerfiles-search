FROM dockercraft/alpine:3.7
MAINTAINER Daniel <daniel@topdevbox.com>

# How-To
 # Local Build: docker build -t mysql-client .
 # Local Run: docker run -it --rm mysql-client mysql

ENV PACKAGES "mysql-client"

RUN apk add --update $PACKAGES \
    && rm -rf /var/cache/apk/*
