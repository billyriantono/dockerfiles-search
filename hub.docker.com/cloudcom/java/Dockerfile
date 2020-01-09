FROM 32bit/debian:jessie

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-i386/jre
ENV JAVA_HOME_LIB $JAVA_HOME/lib

# Installing 32 bits version of JDK for MCC lib
RUN apt-get update
RUN apt-get install -y openjdk-7-jdk
RUN apt-get install -y libssl-dev
RUN apt-get install -y maven

RUN update-alternatives --set java $JAVA_HOME/bin/java