FROM       nanquanyuhao/centos7:demo
MAINTAINER nanquanyuhao <nanquanyuhao@foxmail.com>

ENV JAVA_VERSION 1.7.0
ENV JDK_HOME /usr/lib/jvm/java-1.7.0-openjdk

# Install jre
RUN yum install -y yum-plugin-ovl && \
	yum -y install java-${JAVA_VERSION}-openjdk java-${JAVA_VERSION}-openjdk-devel && \
yum clean all