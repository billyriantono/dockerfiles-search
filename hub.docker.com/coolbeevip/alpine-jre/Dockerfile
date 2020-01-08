FROM coolbeevip/alpine-os:3.7

MAINTAINER coolbeevip <coolbeevip@gmail.com>

# 设置 JAVA 环境变量

ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk \
    PATH=$PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin \
    JAVA_ALPINE_VERSION=8.212.04-r0

RUN set -x && \
    apk update && \
	apk add openjdk8-jre="$JAVA_ALPINE_VERSION"
