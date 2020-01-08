FROM java:openjdk-8-jdk-alpine
MAINTAINER github.com/PengBAI

ARG MAVEN_VERSION=3.5.0

RUN mkdir -p /opt/maven
WORKDIR /opt/maven
RUN wget http://apache.crihan.fr/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
    -O maven.tgz
RUN tar xzf maven.tgz && rm -f maven.tgz

ENV M2_HOME /opt/maven/apache-maven-$MAVEN_VERSION
ENV M2_BIN ${M2_HOME}/bin
ENV PATH ${M2_BIN}:${PATH}

