# Android Dockerfile

FROM ubuntu:18.04

LABEL maintainer="Fabien Hermitte"

# Use unicode
RUN locale-gen C.UTF-8 || true
ENV LANG=C.UTF-8

# Never ask for confirmations
ENV DEBIAN_FRONTEND noninteractive

# Update apt-get
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get update
RUN apt-get dist-upgrade -y

# Installing packages
# Installing packages
RUN apt-get install -y \
  autoconf \
  build-essential \
  bzip2 \
  curl \
  gcc \
  git \
  groff \
  lib32stdc++6 \
  lib32z1 \
  lib32z1-dev \
  lib32ncurses5 \
  libc6-dev \
  libgmp-dev \
  libmpc-dev \
  libmpfr-dev \
  libxslt-dev \
  libxml2-dev \
  m4 \
  make \
  ncurses-dev \
  ocaml \
  openssh-client \
  pkg-config \
  rsync \
  software-properties-common \
  unzip \
  wget \
  zip \
  zlib1g-dev \
  --no-install-recommends

# Install Java
RUN apt-add-repository ppa:openjdk-r/ppa
RUN apt-get update
RUN apt-get -y install openjdk-8-jdk

# Clean Up Apt-get
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get clean

# Download and install Android SDK
ENV ANDROID_SDK_VERSION=4333796
ENV ANDROID_BUILD_TOOLS=29.0.2
ENV ANDROID_PLATFORMS=android-29
ENV ANDROID_MINIMAL_PLATFORM=android-21
ENV ANDROID_EMULATOR_IMAGE=default;armeabi-v7a
ENV ANDROID_VIRTUAL_DEVICE=test

RUN mkdir -p /local/android-sdk && cd /local/android-sdk \
&& curl -o sdk-tools-linux-${ANDROID_SDK_VERSION}.zip -#L "https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_VERSION}.zip" \
&& unzip sdk-tools-linux-${ANDROID_SDK_VERSION}.zip \
&& rm sdk-tools-linux-${ANDROID_SDK_VERSION}.zip
 
# Needed because the executable bits are only set for user, not others
RUN chown -R 1000:1000 /local/android-sdk

# Set the environment variables
ENV ANDROID_HOME /local/android-sdk
ENV PATH ${PATH}:${ANDROID_HOME}/emulator:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

# Download build-tools
RUN yes | sdkmanager \
  "build-tools;${ANDROID_BUILD_TOOLS}" \
  "platforms;${ANDROID_PLATFORMS}" \
  "platform-tools" \
  "emulator" \
  "system-images;${ANDROID_MINIMAL_PLATFORM};${ANDROID_EMULATOR_IMAGE}"

# Accept Android Sdk licences
RUN yes | sdkmanager --licenses && yes | sdkmanager --update

# Export JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/

# Support Gradle
ENV TERM dumb
ENV JAVA_OPTS "-Xms4096m -Xmx4096m"
ENV GRADLE_OPTS "-XX:+UseG1GC -XX:MaxGCPauseMillis=1000"

# Cleaning
RUN apt-get clean

# Add build user account, values are set to default below
ENV RUN_USER mobileci
ENV RUN_UID 5089

RUN id $RUN_USER || adduser --uid "$RUN_UID" \
    --gecos 'Build User' \
    --shell '/bin/sh' \
    --disabled-login \
    --disabled-password "$RUN_USER"

# Fix permissions
RUN chown -R $RUN_USER:$RUN_USER $ANDROID_HOME
RUN chmod -R a+rx $ANDROID_HOME

# Creating project directories prepared for build when running
# `docker run`
ENV PROJECT /project
RUN mkdir $PROJECT
RUN chown -R $RUN_USER:$RUN_USER $PROJECT
WORKDIR $PROJECT

USER $RUN_USER
RUN echo "sdk.dir=$ANDROID_HOME" > local.properties
