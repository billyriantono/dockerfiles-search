FROM java:8-jdk-alpine
MAINTAINER Varun Sharma <varun.sharma0405@gmail.com>

RUN apk --no-cache add curl

RUN mkdir /usr/lib/gradle
ENV GRADLE_VERSION 5.2
ENV GRADLE_HOME /usr/lib/gradle/gradle-${GRADLE_VERSION}
ENV PATH ${PATH}:${GRADLE_HOME}/bin
WORKDIR /usr/lib/gradle
RUN set -x \
  && curl -L -O https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip \
  && unzip gradle-${GRADLE_VERSION}-bin.zip \
  && rm gradle-${GRADLE_VERSION}-bin.zip