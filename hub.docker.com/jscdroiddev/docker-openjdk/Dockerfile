FROM alpine:latest

LABEL maintainer="JscDroidDev"

RUN apk update && apk upgrade
RUN apk --no-cache add openjdk11

ENV JAVA_HOME /usr/lib/jvm/default-jvm
ENV PATH ${PATH}:${JAVA_HOME}/bin
