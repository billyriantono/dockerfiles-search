FROM centos:centos7

MAINTAINER Pluribus Labs Docker Dev <docker-dev@pluribuslabs.com>

RUN yum -y upgrade && \
    yum -y update && \
    yum -y install wget unzip findutils && \
    wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/7u80-b15/jdk-7u80-linux-x64.rpm && \
    wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u102-b14/jdk-8u102-linux-x64.rpm && \
    echo "b516630a940d83b066cf1e6479ec59fe  jdk-7u80-linux-x64.rpm" >> MD5SUM7 && \
    echo "1ffe998845b594c66db2703dd5f60d88  jdk-8u102-linux-x64.rpm" >> MD5SUM8 && \
    md5sum -c MD5SUM7 && \
    md5sum -c MD5SUM8 && \
    rpm -Uvh jdk-7u80-linux-x64.rpm && \
    rpm -Uvh jdk-8u102-linux-x64.rpm && \
    yum -y clean all && \
    rm -f jdk-7u80-linux-x64.rpm jdk-8u102-linux-x64.rpm MD5SUM7 MD5SUM8
