FROM alpine:edge
MAINTAINER Abi Hafshin <abi@hafs.in>

ENV ANDROID_SDK_VERSION 24.4.1
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

RUN echo using path $PATH && \
    apk add --no-cache curl openjdk8 bash libstdc++ && \
    mkdir -p /opt && \
    curl -L http://dl.google.com/android/android-sdk_r${ANDROID_SDK_VERSION}-linux.tgz | tar zxv -C /opt
    

