FROM ubuntu:14.04

MAINTAINER walfud "walfud@aliyun.com"

# Configuration
ENV JAVA_VERSION openjdk-7-jdk
ENV GRADLE_VERSION 2.10
ENV ANDROID_SDK_VERSION 24.4.1
ENV ANDROID_API_VERSION 23
ENV ANDROID_BUILDTOOL_VERSION 23.0.1

# Install basic tool
RUN dpkg --add-architecture i386 && \
    apt-get update -q && \
    apt-get install -qy libncurses5:i386 libstdc++6:i386 zlib1g:i386
RUN apt-get install -qy wget
RUN apt-get install -qy unzip

# Java Environment
RUN apt-get install -qy $JAVA_VERSION

# Gradle Environment
ENV GRADLE_HOME /gradle-${GRADLE_VERSION}
RUN cd / && \
    wget -q https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-all.zip && \
    unzip gradle-${GRADLE_VERSION}-all.zip && \
    rm gradle-${GRADLE_VERSION}-all.zip

# Android Environment
ENV ANDROID_HOME /android_sdk
RUN cd / && \
    mkdir $ANDROID_HOME && \
    cd $ANDROID_HOME && \
    wget -q http://dl.google.com/android/android-sdk_r${ANDROID_SDK_VERSION}-linux.tgz && \
    tar -zxf android-sdk_r${ANDROID_SDK_VERSION}-linux.tgz && \
    rm android-sdk_r${ANDROID_SDK_VERSION}-linux.tgz && \
    mv android-sdk-linux/* . && \
    rm -rf android-sdk-linux && \
    echo y | tools/android update sdk --no-ui --all --filter platform-tools,android-21,android-22,android-${ANDROID_API_VERSION},build-tools-${ANDROID_BUILDTOOL_VERSION},extra-android-support,extra-android-m2repository

# 
ENV PATH=$PATH:$JAVA_HOME/bin:$GRADLE_HOME/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools

WORKDIR /