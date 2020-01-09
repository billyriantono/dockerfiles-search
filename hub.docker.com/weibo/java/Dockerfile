FROM centos:centos7
MAINTAINER Liu Lantao <liulantao@gmail.com>
ENV REFRESHED_AT 2015-09-23

ADD http://yum.liulantao.com/repo/lax-centos.repo /etc/yum.repos.d/lax.repo

RUN yum install -y java
ENV JAVA_HOME /usr/java/latest

CMD ["java"]
