FROM openjdk:8

LABEL maintainer="Adam Hansen"

# -----------------------------------------------------------------------------
# Environment setup
# -----------------------------------------------------------------------------
ENV ANDROID_SDK_URL="https://dl.google.com/android/repository/tools_r25.2.5-linux.zip" \
    ANDROID_APIS="android-28" \
    ANDROID_BUILD_TOOLS_VERSION=28.0.3 \
    GRADLE_VERSION=4.10.3 \
    GRADLE_HOME="/usr/share/gradle" \
    ANDROID_HOME="/opt/android" 

ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION:$GRADLE_HOME/bin

WORKDIR /opt

RUN  \
    dpkg --add-architecture i386 \
    && apt-get -qq update \
    && apt-get -qq install -y wget curl gradle libncurses5:i386 libstdc++6:i386 zlib1g:i386 \
    # Installs Android SDK
    && mkdir android && cd android  \
    && wget -O tools.zip ${ANDROID_SDK_URL} \
    && unzip tools.zip && rm tools.zip \
    && echo y | android update sdk -a -u -t platform-tools,${ANDROID_APIS},build-tools-${ANDROID_BUILD_TOOLS_VERSION} \
    && chmod a+x -R $ANDROID_HOME \
    && chown -R root:root $ANDROID_HOME

# -----------------------------------------------------------------------------
# Cleanup!
# -----------------------------------------------------------------------------
RUN \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get autoremove -y \
    && apt-get clean