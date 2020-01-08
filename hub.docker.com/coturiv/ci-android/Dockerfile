FROM ubuntu:18.04
LABEL maintainer="coturiv@gmail.com"

# Add some core repos
RUN apt-get update && \
	apt-get install -y sudo curl zip openssl build-essential git && \
	apt-get clean;

# Set Android Version
# @sdk-tools    : https://developer.android.com/studio/
# @build-tools  : https://developer.android.com/studio/releases/build-tools?hl=en
# @gradle       : https://gradle.org/releases/
ENV ANDROID_SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip" \
    ANDROID_HOME="/usr/local/android-sdk" \
    ANDROID_VERSION=29 \
    ANDROID_BUILD_TOOLS_VERSION=29.0.0 \
    GRADLE_VERSION=4.10.3

# Install core dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends gnupg flex bison gperf wget zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

  
# Install OpenJDK 8
RUN apt-get update \
    && apt-get install -y --no-install-recommends openjdk-8-jdk \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/oracle-jdk8-installer \
    && java -version

# Set JAVA_HOME
# ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/

# Download Android SDK
RUN mkdir "$ANDROID_HOME" .android \
    && cd "$ANDROID_HOME" \
    && curl -o sdk.zip $ANDROID_SDK_URL \
    && unzip sdk.zip \
    && rm sdk.zip \
    && yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses

# Install Android Build Tool and Libraries
RUN $ANDROID_HOME/tools/bin/sdkmanager --update
RUN $ANDROID_HOME/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" \
    "platforms;android-${ANDROID_VERSION}" \
    "platform-tools"

# Install Gradle
RUN wget https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-all.zip \
    && mkdir /opt/gradle \
    && unzip -d /opt/gradle gradle-${GRADLE_VERSION}-all.zip \
    && rm gradle-${GRADLE_VERSION}-all.zip \
    && ln -s /opt/gradle/gradle-${GRADLE_VERSION}/bin/gradle /usr/bin/gradle \
    && mkdir .gradle \
    && gradle -v
    
