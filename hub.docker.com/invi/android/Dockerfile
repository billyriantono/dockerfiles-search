FROM ubuntu:trusty

MAINTAINER invi "tech@invi.com"
LABEL version="1.0.0"
LABEL description="Android SDK"

ENV DEBIAN_FRONTEND noninteractive

################
# Install Java #
################

ENV JAVA_VERSION 1.8
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle/

RUN \
  apt-get update && \
  apt-get -y install software-properties-common && \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

###################
# Install Android #
###################

# Download Deps
RUN \
  dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install -y unzip wget libstdc++6:i386 libgcc1:i386 zlib1g:i386 libncurses5:i386 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

RUN mkdir -p ${ANDROID_HOME}
WORKDIR ${ANDROID_HOME}

# Download Android SDK
RUN \
  wget -q https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip -O android-tools.zip && \
  unzip android-tools.zip && \
  chown -R root:root tools && \
  rm -f android-tools.zip

RUN yes | sdkmanager --licenses
RUN yes | sdkmanager --update
