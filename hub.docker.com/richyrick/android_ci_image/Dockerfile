FROM openjdk:8-jdk

ENV SDK_TOOLS_URL="https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip" \
    BUILD_TOOLS_VERSION="27.0.3" \
    COMPILE_SDK="27" \
    EMULATOR_SDK="24" \
    ANDROID_HOME=/sdk/ \
    GRADLE_USER_HOME=".gradle" \
    PATH="${PATH}:/sdk/platform-tools/" 

RUN apt-get --quiet update && \
    apt-get install --yes \
    wget \
    tar \ 
    unzip \ 
    lib32stdc++6 \
    lib32z1 \
    kvm \
    file \
    libmagic1 \
    libglu1-mesa \
    mesa-utils \
    libpci3 \
    pciutils \
    qtdeclarative5-dev \
    qtbase5-dev \
    libpulse0 \
    ruby-full \
    gcc \
    make \
    build-essential

RUN gem install fastlane -NV

RUN cp /bin/bash /bin/sh

RUN wget --quiet --output-document=android-sdk.zip ${SDK_TOOLS_URL} && \
    mkdir sdk && \
    unzip android-sdk.zip -d sdk && \
    rm android-sdk.zip

# SDK and related images
RUN echo y | sdk/tools/bin/sdkmanager "extras;google;m2repository" && \
    echo y | sdk/tools/bin/sdkmanager "platforms;android-${COMPILE_SDK}" && \
    echo y | sdk/tools/bin/sdkmanager "platform-tools" && \
    echo y | sdk/tools/bin/sdkmanager "emulator" && \
    echo y | sdk/tools/bin/sdkmanager "build-tools;${BUILD_TOOLS_VERSION}" && \
    echo y | sdk/tools/bin/sdkmanager "extras;android;m2repository" && \
    echo y | sdk/tools/bin/sdkmanager "extras;google;m2repository" && \
    echo y | sdk/tools/bin/sdkmanager "extras;google;google_play_services" && \
    echo y | sdk/tools/bin/sdkmanager "add-ons;addon-google_apis-google-${EMULATOR_SDK}" && \
    echo y | sdk/tools/bin/sdkmanager "system-images;android-${EMULATOR_SDK};google_apis;x86"

RUN wget --quiet --output-document=android-wait-for-emulator https://raw.githubusercontent.com/travis-ci/travis-cookbooks/0f497eb71291b52a703143c5cd63a217c8766dc9/community-cookbooks/android-sdk/files/default/android-wait-for-emulator && \
    chmod +x android-wait-for-emulator
   
