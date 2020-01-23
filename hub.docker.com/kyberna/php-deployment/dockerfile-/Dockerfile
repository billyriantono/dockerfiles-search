FROM openjdk:8-jdk
LABEL maintainer="krzysztof.sinica@gmail.com"

# Based on:
#   https://medium.com/@chima_37359/setup-gitlab-ci-in-flutter-android-project-89f6628828e8

ENV ANDROID_SDK_TOOLS_VERSION="4333796"
ENV ANDROID_COMPILE_SDK_VERSION="28"
ENV ANDROID_BUILD_TOOLS_VERSION="28.0.3"
ENV FLUTTER_VERSION="v1.8.4-dev"
ENV FLUTTER_CHANNEL="dev"

WORKDIR /android

RUN apt-get update \
    && apt-get -y install binutils lib32stdc++6 lib32z1 unzip tar \
    && curl --output sdk-tools.zip "https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_TOOLS_VERSION}.zip" \
    && unzip -d sdk-tools sdk-tools.zip \
    && rm sdk-tools.zip

ENV PATH="${PATH}:/android/sdk-tools/tools/bin/"

RUN echo y | sdkmanager "platforms;android-${ANDROID_COMPILE_SDK_VERSION}" \
    && echo y | sdkmanager "platform-tools" \
    && echo y | sdkmanager "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" \
    && echo y | sdkmanager "ndk-bundle" \
    && yes | sdkmanager --licenses

ENV PATH="${PATH}:/android/sdk-tools/platform-tools/tools/bin"
ENV ANDROID_HOME="/android/sdk-tools/"
ENV ANDROID_NDK_HOME="${ANDROID_HOME}/ndk-bundle"

RUN curl --output flutter-sdk.tar.xz "https://storage.googleapis.com/flutter_infra/releases/${FLUTTER_CHANNEL}/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz" \
    && tar -xf flutter-sdk.tar.xz \
    && rm flutter-sdk.tar.xz 

ENV PATH="${PATH}:/android/flutter/bin"

RUN flutter config --no-analytics \
    && flutter doctor -v

WORKDIR /usr/src/
