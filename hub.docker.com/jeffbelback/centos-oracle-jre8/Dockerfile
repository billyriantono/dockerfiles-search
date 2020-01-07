FROM centos:latest

MAINTAINER Jeff Belback <mail@jeffbelback.me>

# Set JRE_HOME
ENV JRE_HOME /usr/java/default/

RUN yum -y install wget

RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u66-b17/jre-8u66-linux-x64.rpm

RUN echo "f7e8be2384d1d536cc364743ee473364  jre-8u66-linux-x64.rpm" >> MD5SUM && \
    md5sum -c MD5SUM && \
    rpm -Uvh jre-8u66-linux-x64.rpm && \
    yum -y remove wget && \
    rm -f jre-8u66-linux-x64.rpm MD5SUM
