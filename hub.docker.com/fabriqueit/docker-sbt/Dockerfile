FROM docker:stable-dind

MAINTAINER kamaradeivanov

RUN apk add --no-cache git openjdk8 && \
    apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing sbt && \
    sbt sbtVersion

ENV PATH="${PATH}:/usr/lib/jvm/java-1.8-openjdk/bin"
