FROM ubuntu:cosmic
LABEL maintainer="Orhun Birsoy (orhunbirsoy@gmail.com)"

ARG DEBIAN_FRONTEND=noninteractive
RUN dpkg --add-architecture i386 \
    && apt-get update -qq \
    && apt-get install -y --no-install-recommends \
        sudo \
        wget \
        file \
        git \
        subversion \
        vim \
        make \
        nasm \
        ninja-build \
        curl \
        ca-certificates \
        cmake \
        doxygen \
        swig \
        graphviz \
        build-essential \
        tar \
        zip \
        unzip \
        xz-utils \
        software-properties-common \
        openjdk-8-jdk \
        gradle \
        maven \
        libqt5widgets5 \
        python3 \
        python3-dev \
        python3-pip \
        python3-setuptools \
    && apt-get clean

# User setup
RUN groupadd 1001 -g 1001 \
    && groupadd 1000 -g 1000 \
    && groupadd 2000 -g 2000 \
    && groupadd 999 -g 999 \
    && useradd -ms /bin/bash developer -g 1001 -G 1000,2000,999 \
    && printf "developer:developer" | chpasswd \
    && adduser developer sudo \
    && printf "developer ALL= NOPASSWD: ALL\\n" >> /etc/sudoers

RUN pip3 install --no-cache-dir wheel pipenv psutil conan conan-package-tools sesame-package-tools

ENV ANDROID_HOME=/opt/android-sdk \
    ANDROID_NDK_HOME=/opt/android-ndk

ENV ANDROID_SDK_VERSION=4333796 \
    ANDROID_NDK_VERSION=r19b \
    PATH=${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${ANDROID_NDK_HOME}

# android sdk (https://developer.android.com/studio/#downloads)
RUN wget -q --show-progress --progress=bar:force https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_VERSION}.zip -O /tmp/android-sdk-tools.zip \
    && unzip -q /tmp/android-sdk-tools.zip -d ${ANDROID_HOME} \
    && rm /tmp/android-sdk-tools.zip

# install android sdk
RUN mkdir ~/.android && touch ~/.android/repositories.cfg \
    && update-java-alternatives -s java-1.8.0-openjdk-amd64 \
    && yes | sdkmanager --licenses \
    && sdkmanager "emulator" "tools" "platform-tools" \
    && yes | sdkmanager \
      "platforms;android-28" \
      "build-tools;28.0.3" \
      "system-images;android-28;google_apis;x86"

# arm emulator
ENV QT_QPA_PLATFORM=offscreen \
    LD_LIBRARY_PATH=${ANDROID_HOME}/tools/lib64:${ANDROID_HOME}/emulator/lib64:${ANDROID_HOME}/emulator/lib64/qt/lib

# install android ndk
RUN wget -q --show-progress --progress=bar:force https://dl.google.com/android/repository/android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip -O /tmp/ndk.zip \
    && unzip -q /tmp/ndk.zip -d /opt \
    && mv /opt/android-ndk-${ANDROID_NDK_VERSION} ${ANDROID_NDK_HOME} \
    && rm /tmp/ndk.zip

USER developer
WORKDIR /home/developer

RUN mkdir -p /home/developer/.conan \
    && conan user \
    && conan profile new --detect default \
    && conan remote add bincrafters https://api.bintray.com/conan/bincrafters/public-conan \
    && conan remote add sesame https://api.bintray.com/conan/orhun/sesame
