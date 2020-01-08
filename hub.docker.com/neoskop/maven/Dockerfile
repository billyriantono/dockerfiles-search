FROM anapsix/alpine-java:8_jdk_unlimited
LABEL maintainer "devops@neoskop.de"

ENV MAVEN_VERSION 3.5.2
ENV MAVEN_HOME /usr/share/maven

RUN mkdir -p /usr/share \
  && wget -q ftp://mirror.netcologne.de/apache.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz -O - \
    | tar -xzC /usr/share \
  && ln -s /usr/share/apache-maven-$MAVEN_VERSION/bin/mvn /usr/bin/mvn

VOLUME /root/.m2
CMD mvn
