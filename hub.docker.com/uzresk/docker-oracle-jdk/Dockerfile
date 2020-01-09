FROM centos:latest
MAINTAINER uzresk

ENV rpm_url=http://download.oracle.com/otn-pub/java/jdk/8u92-b14/jdk-8u92-linux-x64.rpm

RUN yum install -y wget \
    && wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" -O jdk.rpm ${rpm_url} \
    && rpm -ivh jdk.rpm \
    && rm jdk.rpm
