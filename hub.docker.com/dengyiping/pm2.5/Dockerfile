FROM ubuntu:14.04

MAINTAINER Yiping Deng <scottdeng@live.cn>

# Add sbt repo to sources list
RUN echo "deb http://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list

# Add a repo where OpenJDK can be found.
RUN apt-get update
RUN apt-get upgrade
RUN apt-get install -y git wget software-properties-common
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update

# Auto-accept the Oracle JDK license
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

# Install java
RUN apt-get install -y --force-yes oracle-java8-installer
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


# Install Scala
ENV SCALA_VERSION 2.11.7
ENV SCALA_DEB http://www.scala-lang.org/files/archive/scala-$SCALA_VERSION.deb

RUN \
    wget --quiet --output-document=scala.deb $SCALA_DEB && \
    dpkg -i scala.deb && \
    rm -f *.deb

# Install Scala Build Tool sbt
RUN apt-get install -y --force-yes sbt



#Clone the code
RUN git clone https://github.com/DengYiping/PM2.5.git

# Define working directory
WORKDIR PM2.5/PM2.5server
RUN sbt compile
EXPOSE 8008
CMD ["sbt run"]
