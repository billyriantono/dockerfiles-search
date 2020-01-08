# Ubuntu 14.04.2 LTS
# Oracle Java 8u40 64 bit
# Gradle 2.3
# Git 2.3.5
# Jenkins Swarm Client 1.22

# extend the most recent long term support Ubuntu version
FROM ubuntu

MAINTAINER Applicationa Deploy (http://applicationa.com, deploy@applicationa.com)

WORKDIR /data

RUN apt-key update && apt-get update && apt-get install -y build-essential && apt-get clean
RUN apt-key update && apt-get update && apt-get install -y software-properties-common && apt-get clean

# this is a non-interactive automated build - avoid some warning messages
###ENV DEBIAN_FRONTEND noninteractive

# install wget
RUN apt-key update && apt-get update && apt-get install -y wget && apt-get clean

# install java
# http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html
RUN add-apt-repository ppa:webupd8team/java && \
  apt-key update && apt-get update && \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections && \
  apt-get install -y oracle-java8-installer && \
  apt-get clean

# install git
# http://linuxg.net/how-to-install-git-2-3-4-on-ubuntu-15-04-ubuntu-14-10-ubuntu-14-04-ubuntu-12-04-and-derivative-systems/
RUN add-apt-repository ppa:git-core/ppa && \
  apt-key update && apt-get update && \
  apt-get install -y git && \
  apt-get clean

# install gradle
# http://linuxg.net/how-to-install-gradle-2-1-on-ubuntu-14-10-ubuntu-14-04-ubuntu-12-04-and-derivatives/
RUN add-apt-repository ppa:cwchien/gradle && \
  apt-key update && apt-get update && \
  apt-get install -y gradle && \
  apt-get clean

ADD http://maven.jenkins-ci.org/content/repositories/releases/org/jenkins-ci/plugins/swarm-client/1.22/swarm-client-1.22-jar-with-dependencies.jar /data/

ADD ./jslave.sh /data/

CMD ["./jslave.sh"]