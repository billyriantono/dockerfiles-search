#
# AlpineLinux open jre 8 docker images dockerfile
# @author tekintian
# @url http://github.com/tekintian
# @OPENJDK https://pkgs.alpinelinux.org/contents?branch=edge&name=openjdk8&arch=s390x&repo=community
# @TOMCAT https://wiki.alpinelinux.org/wiki/Tomcat
#

FROM tekintian/alpine:3.8

ENV TOMCAT_MAJOR 9
ENV TOMCAT_VERSION 9.0.13

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH

RUN apk --update add --no-cache curl wget bash openjdk8-jre-base && \
		export JAVA_HOME=$PATH:/usr/lib/jvm/default-jvm && \
		export PATH=${PATH}:${JAVA_HOME}/bin && \
		mkdir -p mkdir -p "$CATALINA_HOME" &&  cd $CATALINA_HOME && \
		wget http://apache.mirrors.tds.net/tomcat/tomcat-9/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz && \
		tar xvzf apache-tomcat-$TOMCAT_VERSION.tar.gz && \
		mv apache-tomcat-$TOMCAT_VERSION/* $CATALINA_HOME/ && \
		rm -rf apache-tomcat-$TOMCAT_VERSION.tar.gz  && \
		apk del curl wget && \
		find ./bin/ -name '*.sh' -exec sed -ri 's|^#!/bin/sh$|#!/usr/bin/env bash|' '{}' +  && \
		\
		# fix permissions (especially for running as non-root)
		# https://github.com/docker-library/tomcat/issues/35
		chmod -R +rX . && \
		chmod 777 logs work  && \
		rm -rf /var/cache/apk/* 

ENTRYPOINT ["/usr/local/tomcat/bin/catalina.sh","run"]

EXPOSE 8080

VOLUME /usr/local/tomcat/webapps/ROOT
WORKDIR /usr/local/tomcat