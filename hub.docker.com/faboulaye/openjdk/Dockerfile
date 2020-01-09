FROM alpine:3.4
MAINTAINER Firdaws Aboulaye "aboufred@gmail.com"

ARG OPEN_JDK_VERSION=8
LABEL java.version=$OPEN_JDK_VERSION

ENV JAVA_HOME /usr/lib/jvm/default-jvm
ENV PATH $JAVA_HOME/bin:$PATH

RUN apk --update add --no-cache openjdk${OPEN_JDK_VERSION} \
  && rm -rf /tmp/* /var/log/* /var/cache/apk/* \
  && java -version
