FROM ubuntu:16.04 
LABEL Maurits Lourens "maurits.lourens@gmail.com"

# Install apt packages RUN apt-get update && apt-get install --yes curl unzip wget
RUN apt-get update && apt-get install -y apt-transport-https curl
RUN curl --silent --location https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y git lib32stdc++6 lib32z1 nodejs s3cmd build-essential openjdk-8-jdk-headless libio-socket-ssl-perl libnet-ssleay-perl wget unzip && apt-get clean && rm -rf /var/lib/apt/lists/*

# Gradle 
ENV GRADLE_VERSION 4.1 
ENV SDK_HOME /usr/local
ENV GRADLE_SDK_URL https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip 
RUN curl -sSL "${GRADLE_SDK_URL}" -o gradle-${GRADLE_VERSION}-bin.zip  \
	&& unzip gradle-${GRADLE_VERSION}-bin.zip -d ${SDK_HOME}  \
	&& rm -rf gradle-${GRADLE_VERSION}-bin.zip
ENV GRADLE_HOME ${SDK_HOME}/gradle-${GRADLE_VERSION} 
ENV PATH ${GRADLE_HOME}/bin:$PATH

# android sdk|build-tools|image 
ENV ANDROID_TARGET_SDK="android-26" \ 
    ANDROID_BUILD_TOOLS="26.0.3" \ 
    ANDROID_SDK_TOOLS="3859397" \ 
    ANDROID_IMAGES="sys-img-armeabi-v7a-android-25,sys-img-armeabi-v7a-android-25" 

ENV ANDROID_SDK_URL https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_TOOLS}.zip 
RUN curl -sSL "${ANDROID_SDK_URL}" -o android-sdk-linux.zip \
    && unzip android-sdk-linux.zip -d android-sdk-linux \
    && rm -rf android-sdk-linux.zip

# Set ANDROID_HOME 
ENV ANDROID_HOME $PWD/android-sdk-linux 
ENV PATH ${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:$PATH 

# licenses 
RUN mkdir $ANDROID_HOME/licenses
RUN echo 8933bad161af4178b1185d1a37fbf41ea5269c55 > $ANDROID_HOME/licenses/android-sdk-license
RUN echo d56f5187479451eabf01fb78af6dfcb131a6481e >> $ANDROID_HOME/licenses/android-sdk-license
RUN echo 84831b9409646a918e30573bab4c9c91346d8abd > $ANDROID_HOME/licenses/android-sdk-preview-license

# Update and install using sdkmanager 
RUN echo yes | $ANDROID_HOME/tools/bin/sdkmanager "tools" "platform-tools"
RUN echo yes | $ANDROID_HOME/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS}"
RUN echo yes | $ANDROID_HOME/tools/bin/sdkmanager "platforms;${ANDROID_TARGET_SDK}"
RUN echo yes | $ANDROID_HOME/tools/bin/sdkmanager "extras;android;m2repository" "extras;google;google_play_services" "extras;google;m2repository"
RUN echo yes | $ANDROID_HOME/tools/bin/sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2"
RUN echo yes | $ANDROID_HOME/tools/bin/sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2"

# Install npm packages 
RUN npm i -g cordova@latest ionic@latest

# mount point for docker
RUN mkdir /app
# ADD /home/maurits/Documents/projects/testApp /app
WORKDIR /app
