FROM gliderlabs/alpine:latest

MAINTAINER Wojciech Wójcik <wojtaswojcik@gmail.com>

ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk

RUN apk -X http://dl-4.alpinelinux.org/alpine/edge/testing --update add openjdk8-jre-base \
    && rm -rf /var/cache/apk/*