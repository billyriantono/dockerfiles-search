FROM openjdk:8-jdk

ARG SDK_VERSION=4333796
ARG SDK_MAJ=28
ARG SDK_MIN=0.3

ENV ANDROID_HOME /usr/local/android 

RUN curl -o /tmp/android-sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-${SDK_VERSION}.zip \
    && unzip /tmp/android-sdk.zip -d ${ANDROID_HOME} \
    && rm /tmp/android-sdk.zip

# add sdkmanager to path
ENV PATH=${PATH}:${ANDROID_HOME}/tools/bin

RUN mkdir ~/.android && echo 'count=0' > ~/.android/repositories.cfg \
    && echo y | sdkmanager "tools" \
    && echo y | sdkmanager "platform-tools" \
    && echo y | sdkmanager "extras;google;m2repository" \
    && echo y | sdkmanager "extras;android;m2repository"  \
    && echo y | sdkmanager "extras;google;google_play_services" \
    && echo y | sdkmanager "platforms;android-${SDK_MAJ}" \
    && echo y | sdkmanager "build-tools;${SDK_MAJ}.${SDK_MIN}" 

    # add platform-tools to path (ex: adb, fastboot)
ENV PATH=${PATH}:${ANDROID_HOME}/platform-tools/bin \
    # add build-tools to path
    PATH=${PATH}:${ANDROID_HOME}/build-tools/${SDK_MAJ}.${SDK_MIN}
