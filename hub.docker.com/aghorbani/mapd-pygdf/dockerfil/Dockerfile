FROM centos:7
MAINTAINER zhuyu@bimwinner.com

RUN yum -y install epel-release.noarch
RUN yum -y install supervisor.noarch curl net-tools 
RUN yum -y install http://tool.airflare.cn/java/jdk-8u162-linux-x64.rpm
RUN sed -i.bak -e 's/^\(securerandom.source=\).*/\1file:\/dev\/urandom/' /usr/java/jdk1.8.0_162/jre/lib/security/java.security
RUN ["bash","-c","echo Asia/Shanghai > /etc/timezone && rm -f /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime"]

ENV JAVA_HOME /usr/java/jdk1.8.0_162/
ENV PATH $JAVA_HOME/bin:$PATH
ENV LC_ALL en_US.UTF-8
