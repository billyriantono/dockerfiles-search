#FROM alpine:3.5
# using frolvlad's alpine since it contains all requirements for Oracle JDK 8 (glibc)
FROM frolvlad/alpine-glibc

# Java
ENV PACKAGE   jdk
ENV MAJOR     8
ENV MINOR     121
ENV BUILD     13
ENV JVM_TEMP  e9e7ea248e2c4826b92b3f075a80e441
# http://download.oracle.com/otn-pub/java/jdk/8u121-b13/jdk-8u121-linux-i586.tar.gz
ENV JAVA_URL  http://download.oracle.com/otn-pub/java/jdk/${MAJOR}u${MINOR}-b${BUILD}/${JVM_TEMP}/${PACKAGE}-${MAJOR}u${MINOR}-linux-x64.tar.gz
# Download, install, 'trim' Java and cleanup
RUN \
  apk add --no-cache --virtual=build-dependencies wget ca-certificates unzip && \
  cd "/tmp" && \
  mkdir /opt && cd /opt && \
  wget --header "Cookie: oraclelicense=accept-securebackup-cookie" ${JAVA_URL} && \
  tar zxf ${PACKAGE}-${MAJOR}u${MINOR}-linux-x64.tar.gz  && \
  ln -s /opt/jdk1.${MAJOR}.0_${MINOR} /opt/jdk && \
  ln -s /opt/jdk1.${MAJOR}.0_${MINOR}/bin/* /usr/bin && \
  rm -rf ${PACKAGE}-${MAJOR}u${MINOR}-linux-x64.tar.gz \
         /opt/jdk/*src.zip \
         /opt/jdk/lib/missioncontrol \
         /opt/jdk/lib/visualvm \
         /opt/jdk/lib/*javafx* \
         /opt/jdk/jre/lib/plugin.jar \
         /opt/jdk/jre/lib/ext/jfxrt.jar \
         /opt/jdk/jre/bin/javaws \
         /opt/jdk/jre/lib/javaws.jar \
         /opt/jdk/jre/lib/desktop \
         /opt/jdk/jre/plugin \
         /opt/jdk/jre/lib/deploy* \
         /opt/jdk/jre/lib/*javafx* \
         /opt/jdk/jre/lib/*jfx* \
         /opt/jdk/jre/lib/amd64/libdecora_sse.so \
         /opt/jdk/jre/lib/amd64/libprism_*.so \
         /opt/jdk/jre/lib/amd64/libfxplugins.so \
         /opt/jdk/jre/lib/amd64/libglass.so \
         /opt/jdk/jre/lib/amd64/libgstreamer-lite.so \
         /opt/jdk/jre/lib/amd64/libjavafx*.so \
         /opt/jdk/jre/lib/amd64/libjfx*.so \
         /tmp/*
ENV JAVA_HOME /opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin
ENV LANG C.UTF-8