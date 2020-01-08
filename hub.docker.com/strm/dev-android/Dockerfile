FROM debian:9.2

LABEL maintainer "opsxcq@strm.sh"

# Java 8 setup & tools
RUN apt-get update && \
    apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    openjdk-8-jdk python python-pip \
    git curl wget maven \
    unzip bzip2 xz-utils unrar-free \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-${JAVA_VERSION}-oracle

# Ant 1.9.7
ENV ANT_VERSION 1.9.9
RUN cd && \
    wget -q https://www.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar -xzf apache-ant-${ANT_VERSION}-bin.tar.gz && \
    mv apache-ant-${ANT_VERSION} /opt/ant && \
    rm apache-ant-${ANT_VERSION}-bin.tar.gz

ENV ANT_HOME /opt/ant
ENV PATH ${PATH}:/opt/ant/bin

# Android SDK r24.4.1 or what user put into $ANDROID_SDK_VERSION

ARG ANDROID_SDK_VERSION
ARG ANDROID_BUILD_TOOLS_VERSION
ENV ANDROID_SDK_VERSION ${ANDROID_SDK_VERSION:-r24.4.1}
ENV ANDROID_BUILD_TOOLS_VERSION ${ANDROID_BUILD_TOOLS_VERSION}

# Add basic i386 architecture software for android 32 bits build-tools
RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoremove -y && \
    apt-get clean

# Installs Android SDK
ENV ANDROID_SDK_FILENAME android-sdk_${ANDROID_SDK_VERSION}-linux.tgz
ENV ANDROID_SDK_URL http://dl.google.com/android/${ANDROID_SDK_FILENAME}
ENV ANDROID_API_LEVELS android-15,android-16,android-17,android-18,android-19,android-20,android-21,android-22,android-23,android-24
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN cd /opt && \
    wget ${ANDROID_SDK_URL} && \
    tar -xzf ${ANDROID_SDK_FILENAME} && \
    rm ${ANDROID_SDK_FILENAME} && \
    echo y | android update sdk --no-ui -a --filter tools,platform-tools,${ANDROID_API_LEVELS},build-tools-23.0.2,build-tools-24.0.3,build-tools-${ANDROID_BUILD_TOOLS_VERSION},extra-android-m2repository,extra-android-support

VOLUME ["/src"]
WORKDIR /src

COPY main.sh /

ENTRYPOINT ["/main.sh"]
CMD ["build"]

# VNC port to connect to the emulator
EXPOSE 5900
