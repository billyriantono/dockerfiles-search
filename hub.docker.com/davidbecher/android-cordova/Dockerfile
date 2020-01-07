FROM ubuntu:16.04

# ------------------------------------------------------
# --- Environment variables
ENV LANG="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8"

ENV ANDROID_HOME /opt/android-sdk-linux

# Install base packages and generate EN US UTF-8 locale

RUN apt-get update -qq \
 && apt-get install -y \
    locales \
    curl \
    wget \
    zip \
    unzip \
    build-essential \
  && locale-gen en_US.UTF-8 \
  && rm -rf /var/lib/apt/lists/*

# Dependencies to execute Android builds

RUN dpkg --add-architecture i386 \
  && apt-get update -qq \
  && apt-get install -y \
    openjdk-8-jdk \
    libc6:i386 \
    libstdc++6:i386 \
    libgcc1:i386 \
    libncurses5:i386 \
    libz1:i386 \
  && rm -rf /var/lib/apt/lists/*

# ------------------------------------------------------
# --- Download Android SDK tools into $ANDROID_HOME

RUN cd /opt \
    && wget -q https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -O android-sdk-tools.zip \
    && unzip -q android-sdk-tools.zip -d ${ANDROID_HOME} \
    && rm android-sdk-tools.zip

ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

# ------------------------------------------------------
# --- Install Android SDKs and other build packages

# Other tools and resources of Android SDK
#  you should only install the packages you need!
# To get a full list of available options you can use:
#  sdkmanager --list

# Accept licenses before installing components, no need to echo y for each component
# License is valid for all the standard components in versions installed from this file
# Non-standard components: MIPS system images, preview versions, GDK (Google Glass) and Android Google TV require separate licenses, not accepted there
RUN yes | sdkmanager --licenses

# Platform tools and SDKs
# Please keep these in descending order!
# The `yes` is for accepting all non-standard tool licenses.
RUN yes | sdkmanager "platform-tools" "platforms;android-25" "build-tools;25.0.3"

# List of most important available packages:
# "platform-tools"
#  "platforms;android-27"
#  "platforms;android-26"
#  "platforms;android-25"
#  "platforms;android-24"
#  "platforms;android-23"
#  "platforms;android-22"
#  "platforms;android-21"
#  "platforms;android-19"
#  "platforms;android-17"
#  "platforms;android-15"
#  "build-tools;27.0.3"
#  "build-tools;27.0.2"
#  "build-tools;27.0.1"
#  "build-tools;27.0.0"
#  "build-tools;26.0.2"
#  "build-tools;26.0.1"
#  "build-tools;25.0.3"
#  "build-tools;24.0.3"
#  "build-tools;23.0.3"
#  "build-tools;22.0.1"
#  "build-tools;21.1.2"
#  "build-tools;19.1.0"
#  "build-tools;17.0.0"
#  "extras;android;m2repository"
#  "extras;google;m2repository"
#  "extras;google;google_play_services"
#  "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2"
#  "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.1"
#  "add-ons;addon-google_apis-google-23"
#  "add-ons;addon-google_apis-google-22"
#  "add-ons;addon-google_apis-google-21"

# ------------------------------------------------------
# --- Install Gradle from PPA

# Gradle PPA
RUN apt-get update -qq \
  && apt-get -y install gradle \
  && gradle -v \
  && rm -rf /var/lib/apt/lists/*

# ------------------------------------------------------
# --- NodeJS and Cordova
RUN curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh \
  && bash nodesource_setup.sh \
  && apt-get update -qq \
  && apt-get install -y nodejs \
  && rm nodesource_setup.sh \
  && rm -rf /var/lib/apt/lists/*

RUN npm install -g cordova@7.0.0 \
  && cordova telemetry off \
  && npm cache clear
