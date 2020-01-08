FROM jeanblanchard/java:8
MAINTAINER Cao Yang <caoy83@qq.com>

# Maven Version
ENV MAVEN_VERSION 3.6.2

# Download and unarchive Maven
RUN apk add --update curl &&\
  mkdir -p /opt &&\
  curl http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-3.6.2-bin.tar.gz -o maven.tar.gz &&\
  gunzip -c maven.tar.gz | tar -xf - -C /opt && rm -f maven.tar.gz &&\
  ln -s /opt/apache-maven-3.6.2 /opt/maven &&\
  apk del curl &&\
  rm -rf /var/cache/apk/*

# Add ./settings.xml /opt/maven/conf/settings.xml

# Set environment
ENV MAVEN_HOME /opt/maven
ENV PATH ${PATH}:${MAVEN_HOME}/bin
