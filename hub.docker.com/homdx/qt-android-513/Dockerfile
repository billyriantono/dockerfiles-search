FROM fedora:31

ARG NDK_VERSION=r20
ARG SDK_INSTALL_PARAMS=platform-tool,build-tools;29.0.2
ARG ANDROID_SDK_ROOT=/android-sdk-linux

RUN dnf update -y && dnf install clang unzip wget time java-1.8.0-openjdk java-1.8.0-openjdk-devel aria2 which patch git make -y

#COPY install-android-sdk /tmp/install-android-sdk
RUN JAVA_HOME=$(dirname $( readlink -f $(which java) )) \
   && JAVA_HOME=$(realpath "$JAVA_HOME"/../) \
   && export JAVA_HOME && echo $JAVA_HOME \
   && wget https://raw.githubusercontent.com/homdx/qtci/513/bin/install-android-sdk --directory-prefix=/tmp \
   &&  chmod u+rx /tmp/install-android-sdk \
   && /tmp/install-android-sdk $SDK_INSTALL_PARAMS

RUN cd /android-sdk-linux/tools/bin/ && ./sdkmanager "platforms;android-21" && cd / && git clone https://github.com/homdx/android_openssl.git  && \
mkdir ~/android && ln -s /android-ndk-r20 ~/android/ndk-bundle && cd /android_openssl && echo time ./build_ssl.sh

ARG ADBCACHE_HASH=8b2d0fd1ed9314070e23b0f6e4c5b5c242670990edcbc2c339a7d4ac8257dad41059796f6ccc8b1bb0037d206bdfe317677fceee800c94f0b619762ca059cbe0

RUN cd /usr/local && curl -SL https://github.com/homdx/qt-android-513/releases/download/1/qt5132-x86-armv7.tar.gz -o qt-5132.tar.gz \
   && set -ex && echo "${ADBCACHE_HASH}  qt-5132.tar.gz" | sha512sum -c  \
   && time tar -xf qt-5132.tar.gz && time rm qt-5132.tar.gz && date && ls -la

RUN echo build OpenSSL from sources && \
export NDK_VERSION=r20 && \
export    ANDROID_NDK_ARCH=arch-arm c && \
export    ANDROID_NDK_EABI=llvm c && \
export    ANDROID_NDK_HOST=linux-x86_64 c && \
export    ANDROID_NDK_TOOLCHAIN_PREFIX=arm-linux-androideabi c && \
export    ANDROID_NDK_TOOLCHAIN_VERSION=4.9 c && \
export DEBIAN_FRONTEND=noninteractive c && \
export ANDROID_NDK_HOME=/android-ndk-r20 && \
cd /android_openssl/ && git checkout 5140  && echo patch -p0 ssl.patch && echo start build ssl && date && time ./build_ssl.sh && date && echo build done && \
ls -la arm

ADD build-android-gradle-project  /usr/bin/

CMD tail -f /bin/true
