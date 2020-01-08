# Minimal docker container to build project
# Image: rabits/qt:5.13-android

FROM ubuntu:18.04
MAINTAINER Alvaro Denis <denisacostaq@gmailcom>

ARG QT_VERSION=5.13.0
ARG NDK_VERSION=r18b
ARG SDK_PLATFORM=android-21
ARG SDK_BUILD_TOOLS=21.1.2
ARG CMAKE_VERSION=3.14.5
ARG SDK_PACKAGES="tools platform-tools"

ENV DEBIAN_FRONTEND=noninteractive \
    QT_PATH=/opt/Qt
ENV QT_ANDROID ${QT_PATH}/${QT_VERSION}/android_armv7
ENV ANDROID_HOME /opt/android-sdk
ENV ANDROID_SDK_ROOT=${ANDROID_HOME} \
    ANDROID_NDK_ROOT=/opt/android-ndk \
    ANDROID_NDK_TOOLCHAIN_PREFIX=arm-linux-androideabi \
    ANDROID_NDK_TOOLCHAIN_VERSION=4.9 \
    ANDROID_NDK_HOST=linux-x86_64 \
    ANDROID_NDK_PLATFORM=${SDK_PLATFORM}
ENV ANDROID_NDK_TOOLS_PREFIX ${ANDROID_NDK_TOOLCHAIN_PREFIX}
ENV QMAKESPEC android-g++
ENV PATH ${QT_ANDROID}/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${PATH}

# Install updates & requirements:
#  * unzip - unpack platform tools
#  * git, openssh-client, ca-certificates - clone & build
#  * locales, sudo - useful to set utf-8 locale & sudo usage
#  * curl - to download Qt bundle
#  * make, openjdk-8-jdk-headless, ant - basic build requirements
#  * libsm6, libice6, libxext6, libxrender1, libfontconfig1, libdbus-1-3, libx11-xcb1 - dependencies of Qt bundle run-file
#  * libc6:i386, libncurses5:i386, libstdc++6:i386, libz1:i386 - dependencides of android sdk binaries
#  * cmake, just an extra tool.
#  * python3, python3-pip, p7zip-full for qli-installer
#  * apt-utils debconf: delaying package configuration, since apt-utils is not installed
RUN dpkg --add-architecture i386 && apt update && apt full-upgrade -y && apt install -y --no-install-recommends \
    wget \
    unzip \
    git \
    openssh-client \
    ca-certificates \
    locales \
    sudo \
    curl \
    make \
    openjdk-8-jdk-headless \
    openjdk-8-jre-headless \
    ant \
    libsm6 \
    libice6 \
    libxext6 \
    libxrender1 \
    libfontconfig1 \
    libdbus-1-3 \
    libx11-xcb1 \
    libc6:i386 \
    libncurses5:i386 \
    libstdc++6:i386 \
    libz1:i386 \
    python3 \
    p7zip-full \
    python3-pip \
    apt-utils \
    && pip3 install requests \
    && apt-get -qq clean \
    && rm -rf /var/lib/apt/lists/*

# Download & unpack Qt toolchains & clean
RUN mkdir -p ${QT_PATH} && cd ${QT_PATH} && wget https://git.kaidan.im/lnj/qli-installer/raw/28d624d43010898320c1d1e40270024966689b14/qli-installer.py \
     && chmod +x qli-installer.py && ./qli-installer.py 5.13.0 linux android android_armv7 && rm qli-installer.py \
     && wget https://raw.githubusercontent.com/denisacostaq/qli-installer/master/qli-installer.py \
     && chmod +x qli-installer.py && ./qli-installer.py 5.13.0 linux android android_armv7 qtcharts \
     && cp -r output/5.13.0 . && rm -rf output qli-installer.py tmp

# Download & unpack android SDK
RUN curl -Lo /tmp/sdk-tools.zip 'https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip' \
    && mkdir -p /opt/android-sdk && unzip -qq /tmp/sdk-tools.zip -d /opt/android-sdk && rm -f /tmp/sdk-tools.zip \
    && yes | sdkmanager --licenses && sdkmanager --update && sdkmanager --verbose "platforms;${SDK_PLATFORM}" "build-tools;${SDK_BUILD_TOOLS}" ${SDK_PACKAGES}

# Download & unpack android NDK
RUN mkdir /tmp/android && cd /tmp/android && curl -Lo ndk.zip "https://dl.google.com/android/repository/android-ndk-${NDK_VERSION}-linux-x86_64.zip" \
    && unzip -qq ndk.zip && mv android-ndk-* $ANDROID_NDK_ROOT && chmod -R +rX $ANDROID_NDK_ROOT \
    && rm -rf /tmp/android

# Download an unpack cmake
RUN wget -qO- https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz | sudo tar xzf - -C /opt/
ENV PATH="/opt/cmake-${CMAKE_VERSION}-Linux-x86_64/bin:$PATH"

RUN bash -cx 'sudo mkdir -p /opt/daqs && sudo chmod -R 777 /opt/daqs && wget -qO- https://github.com/protocolbuffers/protobuf/releases/download/v3.6.1/protobuf-cpp-3.6.1.tar.gz | tar xzf - -C /tmp/ \
    && mkdir -p /tmp/protobuf-3.6.1/build && pushd /tmp/protobuf-3.6.1/build \
    && cmake -Dprotobuf_BUILD_SHARED_LIBS=ON -Dprotobuf_BUILD_TESTS=OFF -Dprotobuf_BUILD_PROTOC_BINARIES=ON -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=${ANDROID_NDK_ROOT}/build/cmake/android.toolchain.cmake -DCMAKE_INSTALL_PREFIX=/opt/daqs/protobuf -DANDROID_NDK=${ANDROID_NDK_ROOT} -DANDROID_TOOLCHAIN=clang -DANDROID_ABI=armeabi-v7a -DANDROID_NATIVE_API_LEVEL=21 -DANDROID_STL=c++_shared -DANDROID_LINKER_FLAGS="-landroid -llog" -DANDROID_CPP_FEATURES="rtti exceptions" /tmp/protobuf-3.6.1/cmake \
    && make -C /tmp/protobuf-3.6.1/build install && popd && mkdir -p /tmp/protobuf-3.6.1/build \
    && pushd /tmp/protobuf-3.6.1/build && sudo apt-get install -y g++ && cmake -Dprotobuf_BUILD_SHARED_LIBS=OFF -Dprotobuf_BUILD_TESTS=OFF -DCMAKE_BUILD_TYPE=Release /tmp/protobuf-3.6.1/cmake \
    && make -C /tmp/protobuf-3.6.1/build && sudo apt-get purge -y g++ && mkdir -p /opt/daqs/protobuf/bin && cp -p /tmp/protobuf-3.6.1/build/protoc /opt/daqs/protobuf/bin/ \
    && rm -rf /tmp/protobuf-3.6.1'

# Reconfigure locale
RUN locale-gen en_US.UTF-8 && dpkg-reconfigure locales

# Add group & user
RUN groupadd -r user && useradd --create-home --gid user user && echo 'user ALL=NOPASSWD: ALL' > /etc/sudoers.d/user

USER user
WORKDIR /home/user
ENV HOME /home/user
