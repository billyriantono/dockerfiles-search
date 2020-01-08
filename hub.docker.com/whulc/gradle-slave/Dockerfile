FROM whulc/java-slave
MAINTAINER Calos Liu <whulc@outlook.com>

RUN apt-get update
RUN apt-get -y upgrade

RUN apt-get install -y wget unzip

RUN wget https://services.gradle.org/distributions/gradle-4.0.1-bin.zip

RUN mkdir /opt/gralde && unzip -d /opt/gradle gradle-4.0.1-bin.zip

RUN export PATH=$PATH:/opt/gradle/gradle-3.4.1/bin
