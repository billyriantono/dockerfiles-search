FROM ubuntu:16.04

LABEL REPO="https://github.com/lacion/docker-android-build"
MAINTAINER Luis Morales <luismmorales@gmail.com>

# System Config
ENV DEBIAN_FRONTEND noninteractive
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

# Android Env Config
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH $PATH:$ANDROID_HOME/tools
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV PATH $PATH:$ANDROID_HOME/build-tools/23.0.3

RUN apt-get update && apt-get install -y locales

RUN locale-gen $LANG
RUN dpkg-reconfigure locales
RUN localedef -i en_US -c -f UTF-8 $LANG

RUN apt-get install -y apt-utils curl \
  git lib32stdc++6 lib32z1 s3cmd build-essential \
  openjdk-8-jdk-headless sendemail libio-socket-ssl-perl libnet-ssleay-perl && \
  rm -rf /var/lib/apt/lists/* && \
  curl -sL https://deb.nodesource.com/setup_7.x | bash - && \
  apt-get install -y nodejs && \
  cd /opt && curl https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz -o android-sdk.tgz && tar xzf android-sdk.tgz && rm android-sdk.tgz && \
  ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | /opt/android-sdk-linux/tools/android update sdk -u -a -t tools,platform-tools,build-tools-23.0.3,android-23,android-25 && \
  npm i -g cordova ionic && \
  npm cache clean && \
  rm -rf /var/lib/apt/lists/* && \
  apt-get clean

WORKDIR /project