FROM openjdk:8-jdk
MAINTAINER Ugva Esteban <ugva@devlabers.com>

RUN mkdir -p /opt/android-sdk-linux && mkdir -p ~/.android && touch ~/.android/repositories.cfg
WORKDIR /opt

ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${PATH}:${ANDROID_HOME}/tools
ENV ANDROID_NDK /opt/android-ndk-linux
ENV ANDROID_NDK_HOME /opt/android-ndk-linux
ENV ANDROID_NDK_VERSION "r20b"
ENV ANDROID_BUILD_TOOLS_VERSION "4333796"


RUN apt-get update && apt-get install -y --no-install-recommends \
    unzip \
    wget \
    swig
RUN apt-get install -y automake autoconf libtool pkg-config gettext perl python flex bison gperf libgmp3-dev make
RUN cd /opt/android-sdk-linux && \
    wget -q --output-document=sdk-tools.zip https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_BUILD_TOOLS_VERSION}.zip && \
    unzip sdk-tools.zip && \
    rm -f sdk-tools.zip && \
    echo y | sdkmanager "build-tools;28.0.2" "platforms;android-28" && \
    echo y | sdkmanager "extras;android;m2repository" "extras;google;m2repository" "extras;google;google_play_services" && \
    sdkmanager "cmake;3.6.4111459"
RUN wget -q --output-document=android-ndk.zip https://dl.google.com/android/repository/android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip && \
    unzip android-ndk.zip && \
    rm -f android-ndk.zip && \
    mv android-ndk-${ANDROID_NDK_VERSION} android-ndk-linux
