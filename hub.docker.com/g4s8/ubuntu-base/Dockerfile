FROM ubuntu:14.04
MAINTAINER Kirill <g4s8.public@gmail.com>
LABEL Description="Base Docker image for Android building based on Ubuntu"

WORKDIR /tmp

ENV DEBIAN_FRONTEND=noninteractive

# Got ubuntu setup here: https://github.com/yegor256/rultor/blob/master/src/docker/Dockerfile

# UTF-8 locale
RUN locale-gen en_US en_US.UTF-8
RUN dpkg-reconfigure locales
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

# Basic Linux tools
RUN apt-get update
RUN apt-get install -y wget unzip

# Got java setup here: https://github.com/yegor256/dockers/blob/master/java8/Dockerfile
RUN apt-get install -y default-jdk
RUN echo "deb http://ppa.launchpad.net/git-core/ppa/ubuntu trusty main" | tee -a /etc/apt/sources.list
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list
RUN echo "deb http://ppa.launchpad.net/natecarlson/maven3/ubuntu precise main" | tee -a /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 E1DF1F24 3DD9F856
RUN apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java8-installer ca-certificates
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# android env
ENV ANDROID_HOME /opt/android
ENV PATH ${PATH}:${ANDROID_HOME}/tools/bin

# prepare
RUN mkdir -pv /root/.android \
  && touch /root/.android/repositories.cfg \
  && mkdir -pv $ANDROID_HOME
COPY packages.txt $ANDROID_HOME/packages.txt
COPY licenses $ANDROID_HOME/licenses

# installing sdk
RUN cd $ANDROID_HOME \
  && wget https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip \
  && unzip sdk-tools-linux-3859397.zip \
  && rm -v sdk-tools-linux-3859397.zip

# update sdk & install packages
RUN cd $ANDROID_HOME \
  && sdkmanager --package_file=packages.txt --verbose \
  && rm -v packages.txt \
  && sdkmanager --licenses \
  && rm -vfr $ANDROID_HOME/emulator/*

RUN rm -rf /tmp/*
RUN rm -rf /root/.ssh
