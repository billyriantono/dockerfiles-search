FROM ubuntu:18.10
ENV ANDROID_HOME="/android-sdk-linux" \
SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip" \
PATH="${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${PATH}"

RUN apt update && apt install -y openjdk-8-jdk curl unzip \
&& mkdir "$ANDROID_HOME" .android \
&& cd "$ANDROID_HOME" \
&& curl -o sdk.zip $SDK_URL \
&& unzip sdk.zip \
&& rm sdk.zip \
&& yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses
