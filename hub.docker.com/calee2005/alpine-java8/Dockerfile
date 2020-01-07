# The Alpine Linux dist with openjdk8 and bash installed
FROM alpine:3.3
MAINTAINER Claude Lee "calee2005@outlook.com"

RUN apk add --update bash openjdk8-jre && rm -rf /var/cache/apk/*

ENV JAVA_HOME=/usr/lib/jvm/default-jvm/jre
