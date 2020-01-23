FROM openjdk:8-alpine

ARG GRADLE_VERSION=3.4.1

RUN set -x && \
    apk add --no-cache bash git wget libressl unzip && \
    mkdir /opt && cd /opt && \
    wget https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip gradle-${GRADLE_VERSION}-bin.zip && \
    rm -f gradle-${GRADLE_VERSION}-bin.zip && \
    ln -s /opt/gradle-${GRADLE_VERSION}/bin/gradle /usr/local/bin/gradle

WORKDIR /root
