################################################################################
#   Este Dockerfile cria uma imagem base  customizada para ionic 3.20          #
# image: dukitan/ionic:3.20                                                    #
################################################################################
FROM node:8.16.2-alpine
 
LABEL plataforma="Node 8.16, OpenJDK 8, Android API 28, Android NDK 17c, Ionic 3.20,"
LABEL ambiente="Build, dev, desenvolvimento, devel"
LABEL maintainer="davidferreira.fz@gmail.com"

ENV SDK_TOOLS_NUMBER "4333796"
ENV BUILD_TOOLS_VERSION="29.0.2"
ENV ANDROID_HOME="/opt/android"
ENV ANDROID_SDK_ROOT="/opt/android"
ENV ANDROID_NDK_HOME="/opt/android/ndk/17.2.4988734/"
ENV PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/$BUILD_TOOLS_VERSION/
ENV CORDOVA_ANDROID_GRADLE_DISTRIBUTION_URL="file:///tmp/gradle-4.10.3-all.zip"


RUN mkdir -p ${ANDROID_HOME}

# Install JDK
RUN apk update && \
    apk add openjdk8 && \
    apk add gradle && \
    apk add git && \
    ln -s /usr/lib/jvm/java-1.8-openjdk/bin/javac /usr/bin/javac && \
    ln -s /usr/lib/jvm/java-1.8-openjdk/bin/jarsigner /usr/bin/jarsigner


# Download and extract Android Tools
RUN wget -q https://dl.google.com/android/repository/sdk-tools-linux-${SDK_TOOLS_NUMBER}.zip -O /tmp/tools.zip && \
    unzip -qq /tmp/tools.zip -d ${ANDROID_HOME} && \
    rm -v /tmp/tools.zip


#Download gradle
RUN wget -q https://downloads.gradle-dn.com/distributions/gradle-4.10.3-all.zip -O /tmp/gradle-4.10.3-all.zip


# Install SDK Packages
RUN mkdir -p ~/.android/ && touch ~/.android/repositories.cfg && \
    yes | ${ANDROID_HOME}/tools/bin/sdkmanager "--licenses" && \
    ${ANDROID_HOME}/tools/bin/sdkmanager "platform-tools" "extras;android;m2repository" "extras;google;m2repository"  \
    "build-tools;$BUILD_TOOLS_VERSION" "platforms;android-28" "ndk;17.2.4988734" && \
    ${ANDROID_HOME}/tools/bin/sdkmanager "--update" && \
    chmod 777 -R $ANDROID_HOME

# Install ionic
RUN npm install -g ionic@3.20 node-gyp node-sass@4.9 cordova @angular/cli --unsafe-perm=true --allow-root


RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.30-r0/glibc-2.30-r0.apk -O /tmp/glibc-2.30-r0.apk && \
    apk add --allow-untrusted /tmp/glibc-2.30-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.30-r0/glibc-bin-2.30-r0.apk -O /tmp/glibc-bin-2.30-r0.apk && \
    apk add --allow-untrusted /tmp/glibc-bin-2.30-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.30-r0/glibc-i18n-2.30-r0.apk -O /tmp/glibc-i18n-2.30-r0.apk && \
    apk add --allow-untrusted /tmp/glibc-i18n-2.30-r0.apk

# Create workspace
RUN mkdir -p /opt/app 
VOLUME ["/opt/app"]
WORKDIR /opt/app
