FROM hlhr202/flutter-ubuntu-base:18.04

ENV ANDROID_VERSION="28"
ENV ANDROID_BUILDTOOLS_VERSION="${ANDROID_VERSION}.0.3"
ENV ANDROID_VERSION_SDK_TOOLS "4333796"
ENV ANDROID_HOME="/opt/android-sdk"

ENV PATH="${ANDROID_HOME}/tools/bin:$PATH"

RUN curl -s -O https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_VERSION_SDK_TOOLS}.zip \
    && mkdir ${ANDROID_HOME} \
    && unzip sdk-tools-linux-${ANDROID_VERSION_SDK_TOOLS}.zip -d ${ANDROID_HOME} \
    && rm sdk-tools-linux-${ANDROID_VERSION_SDK_TOOLS}.zip

RUN mkdir ~/.android \
    && echo 'count=0' > ~/.android/repositories.cfg \
    && yes | sdkmanager --licenses \
    && sdkmanager "tools" "build-tools;${ANDROID_BUILDTOOLS_VERSION}" "platforms;android-${ANDROID_VERSION}" "platform-tools" \
    && yes | sdkmanager --licenses \
    && chown -R root:root /opt