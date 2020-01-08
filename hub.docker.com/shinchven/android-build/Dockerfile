FROM ubuntu:bionic

MAINTAINER shinchven@gmail.com

## Install openjdk and other tools
RUN apt-get update && apt-get upgrade -y && apt-get install git openjdk-8-jdk curl unzip -y

# VERSIONS
ENV SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip" \
    ANDROID_HOME="/usr/local/android-sdk" \
    ANDROID_VERSION=29 \
    ANDROID_BUILD_TOOLS_VERSION=29.0.2

# Download Android SDK
RUN mkdir "$ANDROID_HOME" .android \
    && cd "$ANDROID_HOME" \
    && curl -o sdk.zip $SDK_URL \
    && unzip sdk.zip \
    && rm sdk.zip \
    && yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses \

# Install Android Build Tool and Libraries
&& $ANDROID_HOME/tools/bin/sdkmanager --update \
&& $ANDROID_HOME/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" \
    "platforms;android-${ANDROID_VERSION}" \
    "platform-tools" \
    "ndk-bundle" \
&& mkdir /application

WORKDIR /application
