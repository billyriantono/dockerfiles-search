FROM ubuntu:16.04
MAINTAINER Guilherme Bresser

ENV ANDROID_SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip?hl=pt-br" \
    ANDROID_BUILD_TOOLS_VERSION=27.0.3 \
    ANDROID_APIS="android-27" \
    ANT_HOME="/usr/share/ant" \
    MAVEN_HOME="/usr/share/maven" \
    GRADLE_HOME="/usr/share/gradle" \
    ANDROID_HOME="/opt/android" \
    CORDOVA_VERSION="8.0.0" \
    IONIC_VERSION="3.20.0" \
    CORDOVA_ANDROID_GRADLE_DISTRIBUTION_URL="https://services.gradle.org/distributions/gradle-4.7-bin.zip"
    
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION:$ANT_HOME/bin:$MAVEN_HOME/bin:$GRADLE_HOME/bin

# Install apt packages 
RUN apt-get update && apt-get install --yes curl unzip wget
RUN curl --silent --location https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y  git\ 
                        lib32stdc++6\
                        lib32z1\
                        lib32ncurses5\
                        nodejs\ 
                        s3cmd\
                        build-essential\
                        openjdk-8-jdk-headless\ 
                        sendemail\ 
                        libio-socket-ssl-perl\ 
                        libnet-ssleay-perl\
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Installs Android SDK
RUN mkdir $ANDROID_HOME && cd $ANDROID_HOME
RUN wget -O sdk.zip ${ANDROID_SDK_URL}
RUN unzip -d $ANDROID_HOME/ sdk.zip && rm sdk.zip
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" "platforms;${ANDROID_APIS}" "platform-tools" "extras;google;google_play_services" "extras;google;m2repository"
# RUN mkdir ~/.android && touch ~/.android/repositories.cfg

#GRADLE
RUN wget $CORDOVA_ANDROID_GRADLE_DISTRIBUTION_URL && mkdir /opt/gradle && unzip -d /opt/gradle gradle-4.7-bin.zip
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin::/opt/gradle/gradle-4.7/bin:$PATH
RUN gradle -v

# Install npm packages
RUN npm install -g cordova@$CORDOVA_VERSION ionic@$IONIC_VERSION gulp bower grunt phonegap && npm cache clean
RUN cordova telemetry off

# Create dummy app to build and preload gradle and maven dependencies 
# RUN cd / && echo 'n' | ionic start app && cd /app && ionic platform add android && ionic build android --debug && rm -rf * .??* && rm /root/.android/debug.keystore

RUN echo $PATH
 
WORKDIR /app