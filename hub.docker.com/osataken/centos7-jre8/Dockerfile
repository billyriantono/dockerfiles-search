from centos:7

RUN yum update
RUN yum install wget -y

RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u92-b14/jre-8u92-linux-x64.rpm"

RUN yum localinstall jre-8u92-linux-x64.rpm -y