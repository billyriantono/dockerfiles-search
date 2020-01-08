FROM centos:latest

RUN yum -y upgrade
RUN yum -y install \
  gcc \
  make \
  bison \
  flex \
  libgcc.i686 \
  glibc.i686 \
  glibc-devel.i686 \
  git \
  gcc-c++ \
  libstdc++.i686 \
  net-tools \
  wget

RUN \
  mkdir -p /tmp && wget -P /tmp --no-check-certificate --no-cookies \
  --header "Cookie: oraclelicense=accept-securebackup-cookie" \
  http://download.oracle.com/otn-pub/java/jdk/8u91-b14/jdk-8u91-linux-i586.tar.gz && \
  tar -xzvf /tmp/jdk-8u91-linux-i586.tar.gz -C /opt/ && rm -rf /tmp/jdk-8u91-linux-i586.tar.gz

  RUN \
    mkdir -p /tmp && wget -P /tmp --no-check-certificate --no-cookies \
    --header "Cookie: oraclelicense=accept-securebackup-cookie" \
    http://download.oracle.com/otn-pub/java/jdk/8u91-b14/jre-8u91-linux-i586.tar.gz && \
    tar -xzvf /tmp/jre-8u91-linux-i586.tar.gz -C /opt/ && rm -rf /tmp/jre-8u91-linux-i586.tar.gz

ENV JAVA_HOME /opt/jdk1.8.0_91
ENV JRE_HOME /opt/jre1.8.0_91
