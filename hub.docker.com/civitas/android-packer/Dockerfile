FROM ubuntu
# from https://developer.android.com/studio/#downloads
ENV SDK_TOOLS_VER=4333796 \
    BUILD_TOOLS_VER=28.0.0 \
    APKTOOL_VER=2.3.3
RUN mkdir -p /android-sdk && \
    apt-get update && \
    apt-get install -y openjdk-8-jdk wget curl unzip zip bsdiff python3-pip python3-bcrypt python3-cffi && \
    wget -O /android-sdk/sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-$SDK_TOOLS_VER.zip && \
    unzip /android-sdk/sdk.zip -d /android-sdk && \
    rm -f /android-sdk/sdk.zip && \
    yes | /android-sdk/tools/bin/sdkmanager --licenses && \
    /android-sdk/tools/bin/sdkmanager --install "build-tools;$BUILD_TOOLS_VER" && \
    ln -s /android-sdk/build-tools/$BUILD_TOOLS_VER /android-sdk/build-tools/current && \
    mkdir -p /apktool && \
    wget -O /apktool/apktool.jar https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_$APKTOOL_VER.jar && \
    rm -rf /var/lib/apt/lists/*
