FROM anapsix/alpine-java
MAINTAINER Olivier Perbellini <olivier.perbellini@gmail.com>

RUN set -ex && \ 
    apk upgrade --update && \ 
    apk add --update imagemagick && \ 
    rm -rvf /tmp/* /var/cache/apk/*
