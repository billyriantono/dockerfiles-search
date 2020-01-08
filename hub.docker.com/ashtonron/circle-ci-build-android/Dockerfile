FROM circleci/android:api-26-alpha

ARG ndk_version="r16b"

ENV ANDROID_NDK=${ANDROID_HOME}/android-ndk-${ndk_version} \
    ANDROID_NDK_HOME=${ANDROID_HOME}/android-ndk-${ndk_version}

RUN curl --silent --show-error --location --fail --retry 3 --output /tmp/android-ndk-linux.zip https://dl.google.com/android/repository/android-ndk-${ndk_version}-linux-x86_64.zip && \
    unzip -q /tmp/android-ndk-linux.zip -d ${ANDROID_HOME} && \
    rm /tmp/android-ndk-linux.zip

