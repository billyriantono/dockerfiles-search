FROM java:7-jre
#https://github.com/docker-library/tomcat

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH

RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME

# java
#
# VERSION       Java 8

# use the centos base image provided by dotCloud
FROM centos
MAINTAINER Dedy, dedy@ptdam.com

#ENV JAVA_VERSION 7u55
#ENV BUILD_VERSION b13

# Upgrading system
RUN yum -y upgrade
RUN yum -y install wget

# Downloading Java
RUN wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" "http://cms.ixiasoft.com/downloads/util/java/jdk-7u80-linux-x64.rpm" -O /tmp/jdk-7u80-linux-x64.rpm

RUN yum -y install /tmp/jdk-7u80-linux-x64.rpm

RUN alternatives --install /usr/bin/java jar /usr/java/latest/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000

ENV JAVA_HOME /usr/java/latest


EXPOSE 8080
CMD ["catalina.sh", "run"]
