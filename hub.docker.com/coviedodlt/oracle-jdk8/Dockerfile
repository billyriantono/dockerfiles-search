FROM debian:jessie
MAINTAINER carlos.oviedo@gmail.com

ENV JAVA_VERSION ${JAVA_VERSION:-8}
ENV PACKAGE_VERSION ${PACKAGE_VERSION:-8u66+8u65arm-1~webupd8~1}

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list && \
    echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
    apt-get update && \
	    echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
    apt-get -y -q install oracle-java$JAVA_VERSION-installer=$PACKAGE_VERSION && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/oracle-jdk8-installer
ENV JAVA_HOME /usr/lib/jvm/java-$JAVA_VERSION-oracle
