FROM whulc/java-slave
MAINTAINER Calos Liu <whulc@outlook.com>

RUN apt-get update

RUN apt-get -y upgrade

RUN mkdir /home/jenkins/.m2

ADD settings.xml /home/jenkins/.m2

RUN chown -R jenkins:jenkins /home/jenkins/.m2/

RUN apt-get install -y maven
