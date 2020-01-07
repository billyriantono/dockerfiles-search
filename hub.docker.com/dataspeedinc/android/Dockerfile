FROM openjdk:8

# AWS APT mirrors
RUN sed -i 's+http://security.ubuntu.com/+http://archive.ubuntu.com/+g' /etc/apt/sources.list \
 && sed -i 's+http://archive.ubuntu.com/+http://us-east-1.ec2.archive.ubuntu.com/+g' /etc/apt/sources.list \
 && apt-get update \
 && rm -rf /var/lib/apt/lists/*

# Install git and ssh
RUN apt-get update \
 && apt-get install -y git ssh-client \
 && rm -rf /var/lib/apt/lists/*

# Install packages
RUN apt-get update \
 && apt-get install -y tree gradle \
 && rm -rf /var/lib/apt/lists/*

ENV SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip" \
    ANDROID_HOME="/usr/local/android-sdk" \
    ANDROID_VERSION=26 \
    ANDROID_BUILD_TOOLS_VERSION=26.0.2

# Install Android SDK
RUN mkdir "$ANDROID_HOME" .android \
 && cd "$ANDROID_HOME" \
 && curl -o sdk.zip $SDK_URL \
 && unzip sdk.zip \
 && rm sdk.zip \
 && yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses \
 && $ANDROID_HOME/tools/bin/sdkmanager --update \
 && $ANDROID_HOME/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" \
    "platforms;android-${ANDROID_VERSION}" \
    "platform-tools"

RUN mkdir /application
WORKDIR /application
