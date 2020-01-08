FROM ubuntu:16.04

MAINTAINER PDG Solutions <info@pdg.solutions>

ENV DEBIAN_FRONTEND="noninteractive" \
    NODE_VERSION="10.16.3" \
    NODE_SOURCE="10" \
    NPM_VERSION="6.9.0" \
    IONIC_VERSION="5.3.0" \
    CORDOVA_VERSION="9.0.0" \
    ANDROID_SDK_VERSION="3859397" \
    ANDROID_HOME="/opt/android-sdk" \
    ANDROID_BUILD_TOOLS_VERSION="27.0.0"

# BASIC STUFF
RUN apt-get update \
    && apt-get upgrade \
    && apt-get install -y python-software-properties software-properties-common build-essential git wget curl unzip ruby ruby-dev openjdk-8-jre openjdk-8-jdk gradle \
    && git config --global user.email "info@pdg.solutions" \
    && git config --global user.name "PDG Solutions" \
    && curl -sL https://deb.nodesource.com/setup_$NODE_SOURCE.x -o nodesource_setup.sh \
    && bash nodesource_setup.sh \
    && apt-get install -y nodejs \
    && npm install -g npm@"$NPM_VERSION" \
    && npm install -g cordova@"$CORDOVA_VERSION" ionic@"$IONIC_VERSION" cross-env \
    && npm i -g cordova-res --unsafe-perm \
    && gem install sass \
    && ionic start myApp sidemenu

# ANDROID STUFF
RUN cd /tmp \
    && curl -fSLk https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_VERSION}.zip -o sdk-tools-linux-${ANDROID_SDK_VERSION}.zip \
    && unzip sdk-tools-linux-${ANDROID_SDK_VERSION}.zip \
    && mkdir /opt/android-sdk \
    && mv tools /opt/android-sdk \
    && (while sleep 3; do echo "y"; done) | $ANDROID_HOME/tools/bin/sdkmanager --licenses \
    && $ANDROID_HOME/tools/bin/sdkmanager "platform-tools" \
    && $ANDROID_HOME/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" \
    && apt-get autoremove -y \
    && rm -rf /tmp/sdk-tools-linux-${ANDROID_SDK_VERSION}.zip

ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:/opt/tools

RUN yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses

RUN ln -sf /opt/android-sdk/build-tools/$ANDROID_BUILD_TOOLS_VERSION/zipalign /usr/bin/

WORKDIR myApp
EXPOSE 8100 35729
CMD ["ionic", "lab"]
