FROM amidos/dcind

ENV SCALA_VERSION 2.12.4
ENV SBT_VERSION 1.0.3

ENV HOME /
ENV SBT_HOME /opt/sbt
ENV PATH /sbt/bin:${PATH}

RUN set -x \
    && apk update \
    && apk add openjdk8 bc curl git bash \
    && ( curl -fsL https://github.com/sbt/sbt/releases/download/v${SBT_VERSION}/sbt-${SBT_VERSION}.tgz | tar xfz - ) \
    && mkdir -p /tmp/init/src/main/scala \
    && echo "object Dummy {}" > /tmp/init/src/main/scala/Dummy.scala \
    && echo "scalaVersion := \"${SCALA_VERSION}\"" > /tmp/init/build.sbt \
    && cd /tmp/init \
    && sbt test \
    && cd / \
    && rm -rf /tmp/init \
    && rm -rf /var/lib/apt/lists/*
