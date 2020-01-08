# Pull base image.
FROM sherylynn/android-sdk
MAINTAINER Sherylynn <352281674@qq.com>

# ——————————
# Installs Android NDK
# ——————————

ENV ANDROID_NDK_VERSION r12b
ENV ANDROID_NDK_FILENAME android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip
ENV ANDROID_NDK_URL https://dl.google.com/android/repository/${ANDROID_NDK_FILENAME}
ENV ANDROID_NDK_HOME /opt/android-ndk-${ANDROID_NDK_VERSION}
ENV PATH ${ANDROID_NDK_HOME}:$PATH

RUN cd /opt && \
    wget -q ${ANDROID_NDK_URL} && \
    unzip  ${ANDROID_NDK_FILENAME} && \
    rm ${ANDROID_NDK_FILENAME}