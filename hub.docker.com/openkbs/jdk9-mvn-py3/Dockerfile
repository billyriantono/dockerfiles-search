# use the latest LTS Ubuntu
FROM ubuntu:xenial

MAINTAINER openkbs

ENV DEBIAN_FRONTEND noninteractive

##### update ubuntu and Install Python 3
RUN apt-get update \
  && apt-get install -y automake pkg-config libpcre3-dev zlib1g-dev liblzma-dev \
  && apt-get install -y curl net-tools build-essential libsqlite3-dev sqlite3 bzip2 libbz2-dev git wget unzip vim python3-pip python3-setuptools python3-dev python3-numpy python3-scipy python3-pandas python3-matplotlib \
  && ln -s /usr/bin/python3 /usr/bin/python \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

#### Install Java 9
#### ---------------------------------------------------------------
#### ---- Change below when upgrading version ----
#### ---------------------------------------------------------------
ARG JAVA_MAJOR_VERSION=${JAVA_MAJOR_VERSION:-9}
ARG JAVA_UPDATE_VERSION=${JAVA_UPDATE_VERSION:-0.4}
ARG JAVA_BUILD_NUMBER=${JAVA_BUILD_NUMBER:-11}
ARG JAVA_TOKEN=${JAVA_TOKEN:-c2514751926b4512b076cc82f959763f}

# http://download.oracle.com/otn-pub/java/jdk/9.0.1+11/jdk-9.0.1_linux-x64.tar.gz

#### ---------------------------------------------------------------
#### ---- Don't change below unless you know what you are doing ----
#### ---------------------------------------------------------------
ARG UPDATE_VERSION="${JAVA_MAJOR_VERSION}.${JAVA_UPDATE_VERSION}"
ARG BUILD_VERSION=${JAVA_BUILD_NUMBER}

ENV JAVA_HOME /usr/jdk-${JAVA_MAJOR_VERSION}.${JAVA_UPDATE_VERSION}
ENV PATH $PATH:$JAVA_HOME/bin
ENV INSTALL_DIR /usr

## http://download.oracle.com/otn-pub/java/jdk/9.0.4+11/c2514751926b4512b076cc82f959763f/jdk-9.0.4_linux-x64_bin.tar.gz
# http://download.oracle.com/otn-pub/java/jdk/8u162-b12/0da788060d494f5095bf8624735fa2f1/jdk-8u162-linux-x64.tar.gz
WORKDIR $INSTALL_DIR

#RUN curl -sL --retry 3 --insecure \
#  --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
#  "http://download.oracle.com/otn-pub/java/jdk/${UPDATE_VERSION}+${BUILD_VERSION}/${JAVA_TOKEN}/jdk-${UPDATE_VERSION}_linux-#x64_bin.tar.gz" \
#  | gunzip \
#  | tar x -C /usr/ \
#  && ln -s $JAVA_HOME $INSTALL_DIR/java \
#  && rm -rf $JAVA_HOME/man
  
## bug?
RUN curl -sL --retry 3 --insecure \
  --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
  "http://download.oracle.com/otn-pub/java/jdk/${UPDATE_VERSION}+${BUILD_VERSION}/${JAVA_TOKEN}/jdk-${UPDATE_VERSION}_linux-x64_bin.tar.gz" --output $INSTALL_DIR/jdk-${UPDATE_VERSION}_linux-x64_bin.tar.gz \
  && tar xvf jdk-${UPDATE_VERSION}_linux-x64_bin.tar.gz \
  && ln -s $JAVA_HOME $INSTALL_DIR/java \
  && rm -rf $JAVA_HOME/man jdk-${UPDATE_VERSION}_linux-x64_bin.tar.gz

#### Install Maven 3
ENV MAVEN_VERSION 3.5.0
ENV MAVEN_HOME /usr/apache-maven-$MAVEN_VERSION
ENV PATH $PATH:$MAVEN_HOME/bin
RUN curl -sL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
  | gunzip \
  | tar x -C /usr/ \
  && ln -s $MAVEN_HOME /usr/maven

#### define working directory.
RUN mkdir -p /data
COPY . /data

VOLUME "/data"

WORKDIR /data

#### Define default command.
#ENTRYPOINT ["/bin/bash"]

