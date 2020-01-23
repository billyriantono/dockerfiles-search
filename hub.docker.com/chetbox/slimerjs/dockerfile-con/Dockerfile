FROM centos:7

ENV JAVA_HOME /usr/java/jdk1.8.0_131 
ENV PATH=$PATH:$JAVA_HOME/bin

RUN \
  cd /tmp && \
  curl -O "http://mirrors.linuxeye.com/jdk/jdk-8u131-linux-x64.tar.gz" && \
  tar -xvf jdk-*.tar.gz && \
  rm jdk-*.tar.gz && \
  mkdir -p /usr/java && \
  mv jdk1.* /usr/java && \
  rm -rf $JAVA_HOME/*src.zip && \
  java -version