FROM debian:jessie

MAINTAINER Wojciech Wójcik <wojtaswojcik@gmail.com>

RUN  echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" > /etc/apt/sources.list.d/webupd8team-java.list && \
     echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" >> /etc/apt/sources.list.d/webupd8team-java.list && \
     echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
     apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
     apt-get update && \
     apt-get -y install oracle-java8-installer && \
     apt-get autoremove && \
     rm -rf /var/lib/apt/lists/* && \
     rm -rf /var/cache/oracle-jdk8-installer

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle \
    PATH $PATH:$JAVA_HOME/bin

CMD [""]