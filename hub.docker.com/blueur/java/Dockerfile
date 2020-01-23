FROM alpine:latest

MAINTAINER Blueur

RUN apk update && apk add wget tar
ENV JAVA_HOME=/usr/java
RUN mkdir -p $JAVA_HOME
WORKDIR $JAVA_HOME

ARG JAVA_VERSION
ARG JAVA_UPDATE
ARG JAVA_BUILD

ENV JAVA_VERSION=${JAVA_VERSION:-8} \
	JAVA_UPDATE=${JAVA_UPDATE:-102} \
	JAVA_BUILD=${JAVA_BUILD:-14} \
	JRE_HOME=${JAVA_HOME}/jre \
	PATH=${PATH}:${JAVA_HOME}/bin:${JAVA_HOME}/jre/bin

ENV JDK_TGZ_URL=http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz

RUN wget -O jdk.tar.gz --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" ${JDK_TGZ_URL} \
	&& tar -zxvf jdk.tar.gz --strip-components=1 \
	&& rm jdk.tar.gz
