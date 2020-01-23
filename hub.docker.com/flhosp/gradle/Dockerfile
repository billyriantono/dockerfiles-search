FROM flhosp/centos-jdk
MAINTAINER  Luis Camilo <lcamilo15@gmail.com>

ENV GRADLE_VERSION 2.9

WORKDIR /usr/bin
RUN curl -sLO https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-all.zip && \
  unzip gradle-${GRADLE_VERSION}-all.zip && \
  ln -s gradle-${GRADLE_VERSION} gradle && \
  rm gradle-${GRADLE_VERSION}-all.zip

ENV GRADLE_HOME /usr/bin/gradle
ENV PATH $PATH:$GRADLE_HOME/bin

RUN mkdir /app
WORKDIR /app

