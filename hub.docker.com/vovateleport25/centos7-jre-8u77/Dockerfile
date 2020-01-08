FROM centos:centos7

RUN yum -y install wget

RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u77-b03/jre-8u77-linux-x64.rpm && \
    echo "5559c78c9d8c0bdbfb89d49aa502b56e jre-8u77-linux-x64.rpm" >> MD5SUM && \
    md5sum -c MD5SUM && \
    rpm -Uvh jre-8u77-linux-x64.rpm && \
    rm -f jre-8u77-linux-x64.rpm && \
    rm -f MD5SUM
ENV JAVA_HOME=/usr/java/jre1.8.0_77

