FROM openjdk:8-jdk

ENV ANDROID_HOME ${PWD}/android-sdk

# Apparently there is an upstream error where $SHELL is set to non-existing /usr/bin/bash
# This provides a quick fix.
ENV SHELL /bin/bash

# Install tools needed to download and handle the Android SDK tools
RUN apt-get -y update && apt-get install -y \
    wget \
    unzip \
 && rm -rf /var/lib/apt/lists/*

# Download and unpack the Android SDK tools
RUN wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/tools_r25.2.3-linux.zip && \
    unzip android-sdk.zip -d ${ANDROID_HOME} && \
    rm android-sdk.zip

ENV PATH ${ANDROID_HOME}/tools/bin:${PATH}

# Install android build tools and select SDK versions
RUN echo y | sdkmanager \
    "build-tools;25.0.2" \
    "platforms;android-25"
