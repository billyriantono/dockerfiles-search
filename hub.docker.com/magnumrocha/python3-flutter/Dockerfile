# Docker image based on Debian Stretch
# https://github.com/docker-library/openjdk/blob/master/8/jdk/Dockerfile
# https://github.com/docker-library/buildpack-deps/blob/master/stretch/scm/Dockerfile
# https://github.com/docker-library/buildpack-deps/blob/master/stretch/curl/Dockerfile
FROM openjdk:8-jdk

LABEL maintainer="Magnum Rocha"

ARG BRANCH

ENV INSTALL_DIR="/opt"

ENV ANDROID_TARGET_SDK="26" \
    ANDROID_SDK_BUILD_TOOLS="27.0.3" \
    ANDROID_HOME="$INSTALL_DIR/android-sdk-linux"

ENV ANDROID_SDK_ROOT="$ANDROID_HOME"
ENV FLUTTER_HOME="$INSTALL_DIR/flutter"
ENV DART_SDK_HOME="$FLUTTER_HOME/bin/cache/dart-sdk"

# Install dependencies
RUN apt-get --quiet update --yes
RUN apt-get --quiet install --yes fonts-droid-fallback libstdc++6 lib32stdc++6 lib32z1 libglu1-mesa locales lcov file python3 python python3-dev python3-pip
RUN pip3 install virtualenv

# Add locale
RUN rm -rf /var/lib/apt/lists/*
RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

WORKDIR $INSTALL_DIR

# Install Android SDK

# https://developer.android.com/studio/index.html#command-tools
ARG ANDROID_SDK_BUILD=4333796
ARG ANDROID_SDK_SHA256=92ffee5a1d98d856634e8b71132e8a95d96c83a63fde1099be3d86df3106def9

RUN wget -q -O sdk-tools-linux.zip "https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_BUILD}.zip" \
    && echo "${ANDROID_SDK_SHA256} sdk-tools-linux.zip" | sha256sum -c \
    && unzip -C sdk-tools-linux.zip -d "${ANDROID_HOME}" \
    && rm *.zip

ENV PATH="$ANDROID_HOME/emulator:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools:$DART_SDK_HOME/bin:$FLUTTER_HOME/bin:$PATH"

RUN echo "Accepting licenses"; \
    yes | sdkmanager --licenses

RUN echo "Updating SDK"; \
    sdkmanager --update

RUN echo "Installing packages"; \
    sdkmanager --verbose \
    "platforms;android-$ANDROID_TARGET_SDK" \
    "build-tools;$ANDROID_SDK_BUILD_TOOLS" \
    "platform-tools"  \
    "add-ons;addon-google_apis-google-24" \
    "extras;android;m2repository" \
    "extras;google;m2repository" \
    "extras;google;google_play_services" \
    "extras;google;market_apk_expansion" \
    "extras;google;market_licensing" \
    "ndk-bundle" \
    "lldb;3.0" \
    "cmake;3.6.4111459" \
    "emulator" \
    "system-images;android-25;google_apis;arm64-v8a"

RUN echo "Installed packages"; \
    sdkmanager --list

# Create AVD
RUN echo "Creating AVD"
RUN echo n | avdmanager -v create avd -n pixel -k "system-images;android-25;google_apis;arm64-v8a" -b arm64-v8a -d pixel

# Install Flutter SDK
RUN git clone -b $BRANCH --depth 1 https://github.com/flutter/flutter.git $INSTALL_DIR/flutter
RUN flutter doctor || exit 0
RUN flutter config --no-analytics
