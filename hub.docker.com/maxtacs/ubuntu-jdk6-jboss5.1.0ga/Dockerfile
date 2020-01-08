FROM ubuntu:16.04

MAINTAINER Massimo Scattarella <massimo.scattarella@gmail.com>

# Update OS and install required packages
##########################################
RUN echo "deb http://archive.ubuntu.com/ubuntu xenial main universe" > /etc/apt/sources.list
RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y python-software-properties software-properties-common unzip wget locales \
 && apt-get clean


ENV JAVA_VERSION_MAJOR=6
ENV JAVA_VERSION_MINOR=45
ENV JAVA_VERSION_BUILD=06

ENV JBOSS_VERSION=JBoss-5.1.0.GA
ENV JBOSS_PACKAGE=jboss-5.1.0.GA-jdk6.zip
ENV JBOSS_FOLDER_NAME=jboss-5.1.0.GA

ENV TZ=Europe/Rome
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


# Install JAVA Oracle JDK
##########################################

ADD https://github.com/MassimoScattarella/ubuntu-jdk6-jboss5.1.0ga/raw/master/jdk-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.bin /

RUN chmod +x jdk-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.bin \
 && sync \
 && ./jdk-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.bin \
 && rm jdk-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.bin \
 && mv jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/oracle-jdk-1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} \
 && ln -s /opt/oracle-jdk-1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/java

ENV JAVA_HOME /opt/java
ENV PATH $JAVA_HOME/bin:$PATH


# Install JBoss
##########################################
RUN wget -O ${JBOSS_PACKAGE} https://sourceforge.net/projects/jboss/files/JBoss/${JBOSS_VERSION}/${JBOSS_PACKAGE}/download

RUN unzip ${JBOSS_PACKAGE} \
 && rm ${JBOSS_PACKAGE} \
 && mv ${JBOSS_FOLDER_NAME} /opt/${JBOSS_FOLDER_NAME} \
 && cd /opt/${JBOSS_FOLDER_NAME}/bin && chmod +x *.sh \
 && ln -s /opt/${JBOSS_FOLDER_NAME} /opt/jboss

ENV JBOSS_HOME /opt/jboss


# Run JBoss
##########################################
CMD ["/opt/jboss/bin/run.sh", "-b", "0.0.0.0"]


EXPOSE 8080
EXPOSE 8009