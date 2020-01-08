FROM andresousa/jdk:release-1.0

LABEL maintainer="lucas.eduardo.developer@gmail.com"

# URL do sdkmanager
ENV SDK_MANAGER_URL https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip

# Path do ANDROID_HOME
ENV ANDROID_HOME /opt/android-sdk-linux

# Path do GRADLE_DISTRIBUTION
ENV CORDOVA_ANDROID_GRADLE_DISTRIBUTION_URL https://services.gradle.org/distributions/gradle-4.1-all.zip

# Armazena o path do ANDROID_HOME e do GRADLE_DISTRIBUTION
ENV PATH $PATH:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${CORDOVA_ANDROID_GRADLE_DISTRIBUTION_URL}

# Baixa sdkmanager, gradle e api 29 com o tools e platform
RUN apt-get update -qq && \
    apt-get purge maven maven2 -y && \
    apt-get install wget unzip gradle maven -y && \
    mkdir -p ${ANDROID_HOME} && \
    wget ${SDK_MANAGER_URL} -O android-sdk-tools.zip && \
    unzip -q android-sdk-tools.zip -d ${ANDROID_HOME} && \
    rm android-sdk-tools.zip && \
    yes | sdkmanager --licenses && \
    yes | sdkmanager "tools" \
    "platform-tools" \
    "platforms;android-26" \
    "build-tools;29.0.1" \
    "extras;android;gapid;1" \
    "extras;android;gapid;3" \
    "lldb;3.1" \
    "cmake;3.10.2.4988404" \
    "cmake;3.6.4111459" \
    "extras;google;market_apk_expansion" \
    "extras;google;instantapps" \
    "extras;google;market_licensing" \
    "extras;google;google_play_services" \
    "extras;google;webdriver" \
    "extras;android;m2repository" \
    "extras;google;m2repository"