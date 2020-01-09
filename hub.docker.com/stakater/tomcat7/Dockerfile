FROM stakater/java8-alpine:1.8.0_121
MAINTAINER Hamza <hamza@aurorasolutions.io>

RUN apk -Uuv add wget pwgen ca-certificates

ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.59
ENV CATALINA_HOME /tomcat

# INSTALL TOMCAT
RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
    wget -qO- https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz.md5 | md5sum -c - && \
    tar zxf apache-tomcat-*.tar.gz && \
    rm apache-tomcat-*.tar.gz && \
    mv apache-tomcat* tomcat && \
    rm /var/cache/apk/*

ADD create_tomcat_admin_user.sh /create_tomcat_admin_user.sh
RUN mkdir -p /services/tomcat
ADD run.sh /services/tomcat/run
RUN chmod +x /*.sh
RUN chmod +x /services/tomcat/run

EXPOSE 8080