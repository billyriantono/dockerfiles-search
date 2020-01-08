FROM ubuntu:16.04
LABEL maintainer "David PHAM-VAN <dev.nfet.net@gmail.com>"
LABEL version "1.0"
LABEL description "Android SDK image for gradle builds"

ENV ANDROID_HOME /opt/android-sdk
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools

RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends default-jdk curl unzip git astyle zip librsvg2-bin && \
    mkdir -p ${ANDROID_HOME} && \
    curl https://dl.google.com/android/repository/tools_r25.2.3-linux.zip -o /opt/sdk.zip && \
    unzip -d ${ANDROID_HOME} /opt/sdk.zip && \
    rm -f /opt/sdk.zip && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p ${ANDROID_HOME}/licenses && \
    echo -n '8933bad161af4178b1185d1a37fbf41ea5269c55' > ${ANDROID_HOME}/licenses/android-sdk-license && \
    echo -n '84831b9409646a918e30573bab4c9c91346d8abd' > ${ANDROID_HOME}/licenses/android-sdk-preview-license && \
		echo -n '2f0d1357ae7b730389d07594f0e9b502cc6fe51f' > ${ANDROID_HOME}/licenses/android-googletv-license && \
		echo -n '33b6a2b64607f11b759f320ef9dff4ae5c47d97a' > ${ANDROID_HOME}/licenses/google-gdk-license && \
		echo -n 'e0c19d95f989716a8960e651953886c9fc1f8c0a' > ${ANDROID_HOME}/licenses/mips-android-sysimage-license && \
    ${ANDROID_HOME}/tools/bin/sdkmanager \
    'tools' \
    'platform-tools' \
    'extras;google;m2repository' \
    'extras;android;m2repository' \
    'extras;google;google_play_services' \
    'build-tools;25.0.2' \
    'ndk-bundle' && \
    ${ANDROID_HOME}/tools/bin/sdkmanager --update
