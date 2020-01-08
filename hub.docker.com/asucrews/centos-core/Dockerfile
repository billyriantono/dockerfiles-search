FROM centos:centos7
FROM docker.elastic.co/beats/filebeat:7.3.2
LABEL maintainer="Jeremy M Crews <jeremy.m.crews@gmail.com>"

ENV ELK_VERSION="7.3.2" \
    ELASTICSEARCH="es01"

COPY elastic-7.repo /etc/yum.repos.d/elastic-7.repo
COPY filebeat.yml /usr/share/filebeat/filebeat.yml

USER root
RUN yum -y update &&\
    yum -y install net-tools &&\
    yum -y install bind-utils &&\
    yum -y autoremove &&\
    yum clean all

RUN chown root:filebeat /usr/share/filebeat/filebeat.yml
RUN chmod go-w /usr/share/filebeat/filebeat.yml
