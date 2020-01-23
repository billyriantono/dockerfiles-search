FROM openjdk:8-jdk-stretch

LABEL maintainer="bastien@silence.im"

ENV ANDROID_HOME="/usr/local/bin/android"
ENV PATH="$ANDROID_HOME/emulator:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${PATH}"

RUN mkdir $ANDROID_HOME && \
    wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -O sdk-tools-linux.zip && \
    unzip sdk-tools-linux.zip && \
    mv tools $ANDROID_HOME && \
    rm sdk-tools-linux.zip && \
    mkdir /root/.android/ && \
    touch /root/.android/repositories.cfg && \
    yes | sdkmanager --licenses > /dev/null && \
    wget https://raw.githubusercontent.com/travis-ci/travis-cookbooks/master/community-cookbooks/android-sdk/files/default/android-wait-for-emulator -O /usr/local/bin/android-wait-for-emulator && \
    chmod +x /usr/local/bin/android-wait-for-emulator && \
    sdkmanager "emulator" "platform-tools" "tools" "extras;android;m2repository"
