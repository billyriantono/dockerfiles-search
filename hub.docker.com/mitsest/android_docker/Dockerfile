FROM openjdk:8
MAINTAINER Dimitris Garofalakis<dimitris.garofalakis@atcom.gr>


ENV ANDROID_COMPILE_SDK 28
ENV ANDROID_BUILD_TOOLS 28.0.3
ENV VERSION_SDK_TOOLS 4333796
ENV GRADLE_USER_HOME "/cache/.gradle"
ENV ANDROID_HOME "/android-sdk-linux"

RUN apt-get --quiet update --yes
RUN apt-get --quiet install --yes wget tar unzip lib32stdc++6 lib32z1
RUN wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-${VERSION_SDK_TOOLS}.zip
RUN unzip android-sdk.zip -d ./android-sdk-linux
RUN export PATH=$PATH:$PWD/android-sdk-linux/platform-tools/
RUN mkdir "android-sdk-linux/licenses" || true
RUN mkdir -p /root/.android && touch /root/.android/repositories.cfg
RUN yes | ${ANDROID_HOME}/tools/bin/sdkmanager --licenses
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "add-ons;addon-google_apis-google-24" 
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS}"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "extras;android;m2repository"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "extras;google;m2repository"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "extras;google;google_play_services"
# RUN ${ANDROID_HOME}/tools/bin/sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2"
# RUN ${ANDROID_HOME}/tools/bin/sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "platform-tools"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "platforms;android-${ANDROID_COMPILE_SDK}"
RUN yes | ${ANDROID_HOME}/tools/bin/sdkmanager --licenses
RUN ${ANDROID_HOME}/tools/bin/sdkmanager --update
