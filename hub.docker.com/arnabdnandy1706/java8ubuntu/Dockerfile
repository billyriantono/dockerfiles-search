FROM ubuntu:latest
MAINTAINER Arnab Kumar Nandy
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y postgresql-client
RUN apt-get install -y software-properties-common
RUN apt-get install -y debconf-utils
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get install -y oracle-java8-installer
RUN java -version && javac -version
RUN add-apt-repository -r ppa:webupd8team/java
RUN echo "JAVA_HOME=$(which java)" | tee -a /etc/environment
RUN JAVA_HOME=`which java`
ENV JAVA_HOME=$JAVA_HOME
#RUN source /etc/environment
RUN apt-get install -y openjdk-8-jdk
RUN apt-get install -y openjdk-8-jre
