FROM openjdk:8

ENV GRADLE_VERSION 2.14.1
ENV GRADLE_SDK_URL https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip
ENV GRADLE_HOME /usr/local/gradle-${GRADLE_VERSION}
ENV PATH ${GRADLE_HOME}/bin:$PATH
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools

# Install dependencies:
# Node 8
# zip
# 32-bit support for Android SDK
# Yarn
# Gradle
# Android SDK Tools
# Android SDK dependencies
RUN apt-get update -q && \
    apt-get install -y apt-transport-https && \
    dpkg --add-architecture i386 && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \    
    apt-get update -q && \
    echo "Installing zip" && \
    apt-get -y install zip expect && \
    echo "Installing Node" && \
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs && \
    echo "Installing 32-bit support" && \
    apt-get install -qy --no-install-recommends libstdc++6:i386 libgcc1:i386 zlib1g:i386 libncurses5:i386 && \
    echo "Installing Yarn" && \
    apt-get install -y yarn && \
    echo "Installing Android SDK Tools" && \
    cd /opt \
    && wget -q https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -O tools.zip \
    && mkdir -p ${ANDROID_HOME} \
    && unzip tools.zip -d ${ANDROID_HOME} \
    && rm -f tools.zip && \
    echo "Installing Android dependencies" && \
    $ANDROID_HOME/tools/bin/sdkmanager \
        tools \
        "platform-tools" \
        "build-tools;23.0.1" \
        "build-tools;25.0.2" \
        "build-tools;26.0.1" \
        "build-tools;27.0.3" \
        "platforms;android-23" \
        "platforms;android-25" \
        "platforms;android-26" \
        "platforms;android-27" && \
    yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses && \
    $ANDROID_HOME/tools/bin/sdkmanager --update --verbose

WORKDIR /root
