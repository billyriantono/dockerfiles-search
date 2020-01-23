FROM  adoptopenjdk/openjdk8:jdk8u181-b13-alpine

ENV SBT_VERSION=1.2.6

RUN apk update && apk add bash

RUN curl -sL https://github.com/sbt/sbt/releases/download/v${SBT_VERSION}/sbt-${SBT_VERSION}.tgz | tar xzf - -C /usr/local \
 && ln -s /usr/local/sbt/bin/sbt /usr/local/bin/sbt \
 && sbt exit