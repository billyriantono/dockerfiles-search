FROM        fedora:22

MAINTAINER  Luis Camilo <lcamilo15@gmail.com>

ENV         JDK_URL http://download.oracle.com/otn-pub/java/jdk/8u51-b16/jdk-8u51-linux-x64.tar.gz
ENV         ACTIVATOR_VERSION 1.2.8

# INSTALL JAVA 8
RUN dnf -y update \
    && dnf install -y wget openssl ca-certificates tar unzip \
    && cd /tmp \
    && wget -qO jdk8.tar.gz \
       --header "Cookie: oraclelicense=accept-securebackup-cookie" \
       $JDK_URL \
    && tar xzf jdk8.tar.gz -C /opt \
    && mv /opt/jdk* /opt/java \
    && rm /tmp/jdk8.tar.gz \
    && update-alternatives --install /usr/bin/java java /opt/java/bin/java 100 \
    && update-alternatives --install /usr/bin/javac javac /opt/java/bin/javac 100
