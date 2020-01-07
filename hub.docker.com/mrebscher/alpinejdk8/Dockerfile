FROM alpine:3.4
MAINTAINER mrebscher

ENV JAVA_HOME=/usr/lib/jvm/default-jvm
ENV PATH=${JAVA_HOME}/bin:$PATH

RUN apk update && \
 apk add \
   openjdk8=8.92.14-r1 \
   curl=7.49.1-r0 \
   unzip=6.0-r1 \
   && mkdir /opt
