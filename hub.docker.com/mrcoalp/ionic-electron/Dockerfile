#======================================================================================#
#      IONIC framework capable image with wine to build electron windows packages      #
#======================================================================================#

FROM ubuntu:18.04

# Author
LABEL maintainer "marco.alp120@gmail.com"

# install openjdk-8
RUN apt-get update &&\
    apt-get install -y openjdk-8-jdk wget unzip &&\
    rm -rf /var/lib/apt/lists/*

# download and install Gradle
RUN cd /usr/local &&\
    wget -q https://services.gradle.org/distributions/gradle-5.6.3-bin.zip -O gradle.zip &&\
    unzip gradle.zip &&\
    rm gradle.zip

# set gradle home
ENV GRADLE_HOME=/usr/local/gradle-5.6.3

# set android home
ENV ANDROID_HOME /opt/android-sdk-linux

# download android sdk
# tools, platform-tools and build-tools
RUN mkdir -p ${ANDROID_HOME} &&\
    cd ${ANDROID_HOME} &&\
    wget -q https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -O tools.zip &&\
    unzip tools.zip &&\
    rm tools.zip &&\
    wget -q https://dl.google.com/android/repository/platform-tools_r29.0.4-linux.zip -O platform_tools.zip &&\
    unzip platform_tools.zip &&\
    rm platform_tools.zip &&\
    wget -q https://dl.google.com/android/repository/build-tools_r29.0.2-linux.zip -O build_tools.zip &&\
    unzip build_tools.zip &&\
    rm build_tools.zip

# add android sdk and gradle to path
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/android-10:${GRADLE_HOME}/bin

# accept android licenses
RUN yes | sdkmanager --licenses

# run sdkmanager
RUN sdkmanager "platform-tools" "platforms;android-29" &&\
    sdkmanager "build-tools;29.0.2"

# download and install nodejs
RUN apt-get update &&\
    export DEBIAN_FRONTEND=noninteractive &&\
    apt-get install -y curl &&\
    curl -sL https://deb.nodesource.com/setup_12.x | bash - &&\
    apt-get install -y nodejs

# download and install winehq
RUN apt-get update &&\
    dpkg --add-architecture i386 &&\
    apt-get update &&\
    wget -nc https://dl.winehq.org/wine-builds/winehq.key &&\
    apt-key add winehq.key &&\
    apt-get install -y software-properties-common &&\
    apt-get update &&\
    apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ bionic main' &&\
    apt-get update &&\
    apt-get install -y --install-recommends winehq-stable

# install ionic and cordova
RUN npm i -g ionic &&\
    npm i -g cordova

# cleanup
RUN apt-get update &&\
    apt-get autoremove -y &&\
    apt-get autoclean -y
