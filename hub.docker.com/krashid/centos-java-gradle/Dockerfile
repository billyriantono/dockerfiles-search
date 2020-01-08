FROM centos:7
MAINTAINER ben@krashidbuilt.com

# prepare
WORKDIR /opt
RUN yum -y update
RUN yum -y install wget gcc-c++ make

# oracle jdk 8
RUN wget -O "jdk.rpm" --no-check-certificate --no-cookies \
        --header "Cookie: oraclelicense=accept-securebackup-cookie" \
        --no-verbose http://download.oracle.com/otn-pub/java/jdk/8u66-b17/jdk-8u66-linux-x64.rpm
RUN rpm -ivh jdk.rpm
ENV JAVA_HOME /usr/java/default

# gradle 2.6
RUN wget -qO- https://services.gradle.org/distributions/gradle-2.6-bin.zip | jar xvf /dev/stdin
ENV GRADLE_BIN /opt/gradle-2.6/bin
RUN chmod +x ${GRADLE_BIN}/gradle
ENV PATH $PATH:${GRADLE_BIN}


# clean
RUN rm -rf *.rpm
RUN rm -rf *.zip
RUN yum -y clean all
