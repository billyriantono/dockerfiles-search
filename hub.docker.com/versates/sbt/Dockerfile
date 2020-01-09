FROM openjdk:11-jdk-slim

LABEL maintainer="Versates <docker@versates.com>"

ARG SCALA_VERSION="2.13.1"
ARG SBT_VERSION="1.3.4"
ARG APPUSER="versa"

ENV SCALA_HOME="/usr/local/scala-${SCALA_VERSION}"

RUN apt-get update -qq; \
    apt-get autoremove -qq --purge; \
    apt-get install -qq --no-install-recommends wget fakeroot; \
    wget -qO- https://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz | tar xfz - -C /usr/local && \
    rm -f ${SCALA_HOME}/bin/*.bat && \
    ln -s ${SCALA_HOME}/bin/scala /usr/local/bin/scala; \
    wget -q https://dl.bintray.com/sbt/debian/sbt-${SBT_VERSION}.deb && \
    dpkg -i sbt-${SBT_VERSION}.deb && \
    rm -f sbt-${SBT_VERSION}.deb; \
    adduser --quiet --system --group --home /usr/local/${APPUSER} --shell /bin/bash ${APPUSER} && \
    install -d -m 0755 -o ${APPUSER} -g ${APPUSER} /var/log/${APPUSER}; \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*

USER ${APPUSER}
WORKDIR /usr/local/${APPUSER}

RUN sbt sbtVersion; \
    mkdir project; \
    echo "scalaVersion := \"${SCALA_VERSION}\"" | tee build.sbt; \
    echo "sbt.version=${SBT_VERSION}" | tee project/build.properties; \
    echo "case object Temp" | tee Temp.scala; \
    sbt compile; \
    rm -rf *
