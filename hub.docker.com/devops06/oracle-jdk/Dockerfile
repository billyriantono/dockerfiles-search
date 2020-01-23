FROM devops06/centos:7
MAINTAINER zhfang@dataman-inc.com

RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u11-b12/jdk-8u11-linux-x64.rpm \
    && rpm -ivh jdk-8u11-linux-x64.rpm \
    && rm jdk-8u11-linux-x64.rpm

