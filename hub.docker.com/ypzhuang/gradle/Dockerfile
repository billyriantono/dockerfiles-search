FROM ypzhuang/jdk_alpine

MAINTAINER ypzhuang <sunbei914914@msn.com>

ENV GRADLE_VERSION 3.5
ENV GRADLE_DOWNLOAD_URL https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip
ENV PATH $PATH:/opt/gradle-${GRADLE_VERSION}/bin

WORKDIR /opt

RUN apk update  && \
    apk --no-cache add openssl 

RUN wget -O gradle.zip  $GRADLE_DOWNLOAD_URL && unzip gradle.zip && rm gradle.zip


