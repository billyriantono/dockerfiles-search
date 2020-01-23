FROM alpine:3.11

LABEL maintainer="fx.jianglin@126.com"

ENV LANG C.UTF-8
ENV TZ Asia/Shanghai

RUN { \
    echo '#!/bin/sh'; \
    echo 'set -e'; \
    echo; \
    echo 'dirname "$(dirname "$(readlink -f "$(which java)")")"'; \
    } > /usr/local/bin/docker-java-home \
    && chmod +x /usr/local/bin/docker-java-home

ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-11-openjdk/bin

ENV JAVA_VERSION 11.0.5
ENV JAVA_ALPINE_VERSION 11.0.5_p10-r0

RUN set -x \
    && apk update \
    && apk add --no-cache \
    openjdk11-jre="$JAVA_ALPINE_VERSION" \
    tzdata ttf-dejavu tini bash \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && [ "$JAVA_HOME" = "$(docker-java-home)" ]