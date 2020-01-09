FROM openjdk:8-alpine

LABEL maintainer="Vijay Raghavan Aravamudhan<vraravam@thoughtworks.com>"

ARG JMETER_VERSION=4.0

ENV JMETER_HOME /jmeter/apache-jmeter-${JMETER_VERSION}/
ENV JMETER_BIN  ${JMETER_HOME}/bin
ENV MIRROR_HOST https://archive.apache.org/dist/jmeter
ENV JMETER_DOWNLOAD_URL ${MIRROR_HOST}/binaries/apache-jmeter-${JMETER_VERSION}.tgz

RUN apk update \
    && apk add --no-cache --update wget unzip ca-certificates openssl \
    && rm -rf /var/cache/apk/* \
    && mkdir /jmeter \
    && cd /jmeter/ \
    && wget ${JMETER_DOWNLOAD_URL} \
    && tar -xzf apache-jmeter-$JMETER_VERSION.tgz \
    && rm -f apache-jmeter-$JMETER_VERSION.tgz

ENV PATH $PATH:$JMETER_BIN

WORKDIR /
