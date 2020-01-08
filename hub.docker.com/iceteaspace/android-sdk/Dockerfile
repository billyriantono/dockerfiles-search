FROM  openjdk:8-alpine
LABEL maintainer "Duong Hong Hung <monszdev@gmail.com>"

ENV ANDROID_HOME=/var/opt/android-sdk
ENV ANDROID_SDK_ROOT=${ANDROID_HOME}
ENV PATH=$PATH:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

ARG ANDROID_SDK_TOOL=4333796

RUN apk update && \
    apk add unzip wget

RUN mkdir -p ~/.android && \
    touch ~/.android/repositories.cfg && \
    wget https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_TOOL}.zip && \
    unzip sdk-tools-linux-${ANDROID_SDK_TOOL}.zip -d ${ANDROID_HOME} && \
    rm sdk-tools-linux-${ANDROID_SDK_TOOL}.zip

RUN yes | sdkmanager --licenses
RUN sdkmanager --update && \
    sdkmanager "tools" "platform-tools" && \
    sdkmanager "platforms;android-28" "build-tools;28.0.3" && \
    sdkmanager "extras;android;m2repository" "extras;google;m2repository" && \
    sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2" && \
    sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2"
