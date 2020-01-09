FROM flexys/dcind

MAINTAINER Joe Heath <joe.heath@flexys.co.uk>

ENV SBT_VERSION 1.0.0
ENV SBT_HOME /usr/local/sbt
ENV PATH ${PATH}:${SBT_HOME}/bin

RUN apk add --update bash
RUN apk add --update curl

RUN curl -sL "https://github.com/sbt/sbt/releases/download/v1.0.0/sbt-1.0.0.tgz" \
    | gunzip \
    | tar -x -C /usr/local && \
    echo -ne "- with sbt $SBT_VERSION\n" >> /root/.built

run apk --update add  openjdk8

RUN sbt update
