FROM anapsix/alpine-java
MAINTAINER sumeet rohatgi 

RUN apk add --update curl git unzip python3 py-pip && pip install -U py4j

ENV PYTHONHASHSEED 0
ENV PYTHONIOENCODING UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV SPARK_VERSION 1.6.0
ENV SPARK_PACKAGE spark-${SPARK_VERSION}-bin-hadoop2.6
ENV SPARK_HOME /usr/${SPARK_PACKAGE}
ENV PATH $PATH:${SPARK_HOME}/bin
RUN curl -sL --retry 3 \
  "http://d3kbcqa49mib13.cloudfront.net/${SPARK_PACKAGE}.tgz" \
  | gunzip \
  | tar x -C /usr/

WORKDIR ${SPARK_HOME}
