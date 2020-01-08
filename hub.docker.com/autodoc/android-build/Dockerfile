FROM openjdk:8-jdk

MAINTAINER Danilo Correa <dcorrea@autodoc.com.br>

WORKDIR /opt

ENV ANDROID_COMPILE_SDK 28
ENV ANDROID_BUILD_TOOLS 28.0.3
ENV ANDROID_SDK_TOOLS 4333796


RUN apt-get update -y --no-install-recommends \
    && apt-get upgrade -y

RUN apt-get install wget tar unzip lib32stdc++6 lib32z1 -y

RUN mkdir /root/.android \
    && touch /root/.android/repositories.cfg

RUN wget \
    --quiet \
    --output-document=android-sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_TOOLS}.zip \
    && unzip -d android-sdk-linux android-sdk.zip

RUN echo y | android-sdk-linux/tools/bin/sdkmanager "platforms;android-${ANDROID_COMPILE_SDK}" >/dev/null \
    && echo y | android-sdk-linux/tools/bin/sdkmanager "platform-tools" >/dev/null \
    && echo y | android-sdk-linux/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS}" >/dev/null