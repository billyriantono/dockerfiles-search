FROM openjdk:latest
MAINTAINER Joe Moore <jpvlsmv@gmail.com>

# Chased down from https://github.com/samtstern/android-vagrant/blob/master/docker/android-sdk/Dockerfile

RUN dpkg --add-architecture i386 && apt-get update && apt-get install -yq libstdc++6:i386 zlib1g:i386 libncurses5:i386 ant maven --no-install-recommends

RUN curl -L https://dl.google.com/android/repository/tools_r25.2.3-linux.zip | tar xz -C /usr/local
ENV ANDROID_HOME /usr/local/android-sdk-linux

ENV ANDROID_SDK_COMPONENTS platform-tools,build-tools-21.1.2,android-21,extra-android-support
RUN echo y | ${ANDROID_HOME}/tools/android update sdk --no-ui --all --filter "${ANDROID_SDK_COMPONENTS}"

ENV PATH $PATH:${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools