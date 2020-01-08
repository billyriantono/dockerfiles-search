FROM drokar/centos-s6:latest
MAINTAINER Charles Drolet-Achkar <charles.drokar@gmail.com>

# Setting environment variables
ENV \
  JAVA_VERSION=8u60 \
  BUILD_NUMBER=b27 \
  JAVA_HOME=/usr/bin/java \
  PATH=$JAVA_HOME:$PATH

# Downloading Java
RUN wget -q --no-cookies --no-check-certificate --header \
  "Cookie: oraclelicense=accept-securebackup-cookie" \
  "http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-$BUILD_NUMBER/jdk-$JAVA_VERSION-linux-x64.rpm" \
  -O /tmp/jdk-linux-x64.rpm && \
  yum -y install /tmp/jdk-linux-x64.rpm && \
  rm -f /tmp/jdk-linux-x64.rpm
