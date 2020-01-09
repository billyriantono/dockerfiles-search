FROM ubuntu:18.04
LABEL MAINTAINER Cihad Guzel <cguzelg@gmail.com>

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV ANDROID_HOME /root/android
ENV PATH ${PATH}:${ANDROID_HOME}/tools


#java
RUN echo Install Java... && \
apt-get update && \
apt-get install -y gnupg && \
apt-get install -y --no-install-recommends locales && \
locale-gen en_US.UTF-8 && \
apt-get dist-upgrade -y && \
apt-get --purge remove openjdk* && \
echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections && \
echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" > /etc/apt/sources.list.d/webupd8team-java-trusty.list && \
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
apt-get update && \
apt-get install -y --no-install-recommends oracle-java8-installer oracle-java8-set-default && \
apt-get clean all

#nodejs
RUN apt install -y nodejs npm && \
echo Install NodeJs... && \
nodejs --version && \
echo Install npm... && \
npm --version

#cordova
RUN echo Install cordova... && \
npm install -g cordova && \
cordova telemetry off

#gem
RUN echo Install gem... && \
apt-get install -y rubygems
 
#gradle
RUN echo Install gradle... && \
apt-get install -y gradle && \
mkdir ~/.gradle && \
echo 'org.gradle.daemon=true' >> ~/.gradle/gradle.properties

#android for build
RUN echo Install sdk... && \
mkdir ${ANDROID_HOME} && \
cd ${ANDROID_HOME} && \
wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip && \
unzip sdk-tools-linux-4333796.zip && \
rm sdk-tools-linux-4333796.zip && \
${ANDROID_HOME}/tools/bin/sdkmanager --update && \
yes | ${ANDROID_HOME}/tools/bin/sdkmanager "platforms;android-27" "build-tools;27.0.3" "extras;google;m2repository" "extras;android;m2repository" && \
yes | ${ANDROID_HOME}/tools/bin/sdkmanager --licenses

#git 
RUN echo Install git... && \
apt-get install -y git
