FROM maven:3-jdk-8-alpine

MAINTAINER lciclcAzz <lciclcAzz[AT]gmail.com>

ENV LANG C.UTF-8
ENV BUILD_PATH /build

COPY config/setting.xml /root/.m2/
# COPY config/setting.xml /usr/share/maven/ref/
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh

WORKDIR $BUILD_PATH
