FROM openjdk:8-jdk-alpine
MAINTAINER <lpz>

RUN apk add curl wget net-tools && curl -SL http://archive.apache.org/dist/hadoop/core/hadoop-3.2.1/hadoop-3.2.1.tar.gz | tar -zxC /opt/ && rm -rf /opt/hadoop-3.2.1/share/doc
