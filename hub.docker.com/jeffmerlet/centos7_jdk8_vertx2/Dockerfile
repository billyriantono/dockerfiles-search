# Autor Jeff Merlet
# version 0.0.1
#
# Image with CentOS 7 latest, Java JDK 8.31 and Vertx 2.1.5

FROM centos:latest

MAINTAINER Jeff Merlet "jeff@teforia.com"

# Upgrades system
RUN yum -y update && yum clean all
RUN yum -y upgrade

# Installs wget
RUN yum -y install wget

# Installs tar
RUN yum -y install tar

# Downloads Java
RUN wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" "https://download.oracle.com/otn-pub/java/jdk/8u31-b13/jdk-8u31-linux-x64.rpm" -O /tmp/jdk-8-linux-x64.rpm

# Installs Java
RUN yum -y install /tmp/jdk-8-linux-x64.rpm
RUN alternatives --install /usr/bin/java jar /usr/java/latest/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
ENV JAVA_HOME /usr/java/latest
RUN java -version

# Downloads Vertx
RUN wget "https://bintray.com/artifact/download/vertx/downloads/vert.x-2.1.5.tar.gz" -O /tmp/vertx-2.tar.gz

# Installs Vertx
RUN mkdir -p /usr/local/vertx
RUN cd /usr/local/vertx
RUN tar -zxvf /tmp/vertx-2.tar.gz -C /usr/local/vertx
ENV PATH /usr/local/vertx/vert.x-2.1.5/bin:$PATH
RUN vertx version


# Increase log level of hazelcast, so we can see some useful information
#RUN sed -i "s/\(com\.hazelcast\.level=\).*\$/\1INFO/" /usr/local/vertx/conf/logging.properties


