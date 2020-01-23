FROM centos

MAINTAINER Arun Bakt

RUN yum update -y && \
    curl --insecure --junk-session-cookies --location --remote-name --silent --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u65-b17/server-jre-8u65-linux-x64.tar.gz  && \
    mkdir -p /usr/java/default && \
    tar xfz server-jre-8u65-linux-x64.tar.gz -C /usr/java/default && \
    alternatives --install /usr/bin/java java /usr/java/default/jdk1.8.0_65/bin/java 1 && \
    alternatives --install /usr/bin/jar  jar  /usr/java/default/jdk1.8.0_65/bin/jar  1 && \
    rm server-jre-8u65-linux-x64.tar.gz && \
    yum clean all

ENV JAVA_HOME=/usr/java/default/jdk1.8.0_65 \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8

RUN yum -y install wget \
		tar \
		unzip \
	&& yum -y clean all

# Gradle
WORKDIR /usr/bin
RUN wget https://services.gradle.org/distributions/gradle-2.11-all.zip && \
    unzip gradle-2.11-all.zip && \
    ln -s gradle-2.11 gradle && \
    rm gradle-2.11-all.zip
# Set Appropriate Environmental Variables
ENV GRADLE_HOME /usr/bin/gradle
ENV PATH $PATH:$GRADLE_HOME/bin 
