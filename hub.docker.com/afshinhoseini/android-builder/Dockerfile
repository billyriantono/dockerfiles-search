FROM openjdk:8-jdk

RUN apt-get --quiet update --yes
RUN apt-get --quiet install --yes wget tar unzip lib32stdc++6 lib32z1
RUN wget --quiet --output-document=android-sdk.tgz https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
RUN tar --extract --gzip --file=android-sdk.tgz
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter android-24
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter android-17
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter platform-tools
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter build-tools-24.0.3
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter build-tools-25.0.0
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-android-m2repository
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-google-google_play_services
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-google-m2repository
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter sys-img-armeabi-v7a-android-17
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter sys-img-armeabi-v7a-android-22
RUN echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter sys-img-armeabi-v7a-android-24

ENV ANDROID_HOME ${PWD}/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/platform-tools/:${ANDROID_HOME}/tools

RUN which android
RUN which adb
