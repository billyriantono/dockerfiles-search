FROM openjdk:8-alpine

ARG ANDROID_SDK_TOOLS="4333796"

ENV ANDROID_HOME "/opt/android"
ENV GLIBC_VERSION "2.28-r0"

# Install required dependencies
RUN apk add --no-cache --virtual=.build-dependencies wget unzip ca-certificates grep sed && \
    wget -q https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub -O /etc/apk/keys/sgerrand.rsa.pub && \
    wget -q https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk -O /tmp/glibc.apk && \
    wget -q https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk -O /tmp/glibc-bin.apk && \
    apk add --no-cache /tmp/glibc.apk /tmp/glibc-bin.apk && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/*

# Download and extract Android Tools
RUN wget --quiet https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_TOOLS}.zip -O /tmp/android-sdk-tools.zip && \
    mkdir -p ${ANDROID_HOME} && \
    unzip -qq /tmp/android-sdk-tools.zip -d ${ANDROID_HOME} && \
    rm /tmp/android-sdk-tools.zip

ENV PATH ${PATH}:${ANDROID_HOME}/platform-tools/

# Initialize SDK manager
RUN mkdir -p /root/.android/ && touch /root/.android/repositories.cfg && \
    yes | ${ANDROID_HOME}/tools/bin/sdkmanager "--licenses" && \
    ${ANDROID_HOME}/tools/bin/sdkmanager "--update" >/dev/null

# Install SDK Packages
RUN ${ANDROID_HOME}/tools/bin/sdkmanager \
    "tools" \
    "platform-tools" \
    "emulator" \
    "platforms;android-28" \
    "platforms;android-27" \
    "platforms;android-26" \
    "platforms;android-25" \
    "build-tools;28.0.3" \
    "build-tools;28.0.2" \
    "build-tools;27.0.3" \
    "build-tools;27.0.2" \
    "build-tools;27.0.1" \
    "build-tools;26.0.2" \
    "build-tools;26.0.1" \
    "build-tools;26.0.0" \
    "build-tools;25.0.3" \
    "build-tools;25.0.2" \
    "build-tools;25.0.1" \
    "build-tools;25.0.0" \
    >/dev/null