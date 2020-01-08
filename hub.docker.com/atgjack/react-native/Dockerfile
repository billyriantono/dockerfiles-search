FROM atgjack/node-java
MAINTAINER atgJack, https://github.com/atgJack/dockerfiles

# Environmental Variables
ENV ANDROID_VERSION=24.4.1
ENV ANDROID_URL=http://dl.google.com/android/android-sdk_r${ANDROID_VERSION}-linux.tgz
ENV ANDROID_HOME=/usr/android
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

# Install Watchman
# rm -rf /node-${VERSION}.tar.gz /SHASUMS256.txt.asc /node-${VERSION} ${RM_DIRS} \
RUN apk add --update git tar ca-certificates curl && update-ca-certificates
RUN git clone https://github.com/facebook/watchman.git \
  && cd watchman \
  && git checkout v4.7.0  # the latest stable release \
  && ./autogen.sh \
  && ./configure \
  && make \
  && make install

# Install Android SDK
RUN curl -fSL -o android.tgz $ANDROID_URL && \
    mkdir -p /usr/android && \
    tar -xzf android.tgz -C /usr/android --strip-components=1


RUN echo "y" | android update sdk -u -a --filter tools && \
    echo "y" | android update sdk -u -a --filter platform-tools && \
    echo "y" | android update sdk -u -a --filter extra-android-support && \
    echo "y" | android update sdk -u -a --filter extra-android-m2repository && \
    echo "y" | android update sdk -u -a --filter extra-google-google_play_services && \
    echo "y" | android update sdk -u -a --filter extra-google-m2repository && \
    echo "y" | android update sdk -u -a --filter extra-google-analytics_sdk_v2

# https://github.com/yongjhih/docker-android/blob/master/ubuntu-openjdk-8-android-all/Dockerfile
RUN echo "y" | android update sdk -u -a --filter android-23 && \
    echo "y" | android update sdk -u -a --filter build-tools-23.0.2 && \
    echo "y" | android update sdk -u -a --filter build-tools-23.0.1 && \
    echo "y" | android update sdk -u -a --filter build-tools-23.0.0 && \
    echo "y" | android update sdk -u -a --filter android-22 && \
    echo "y" | android update sdk -u -a --filter build-tools-22.0.1 && \
    echo "y" | android update sdk -u -a --filter build-tools-22.0.0 && \
    echo "y" | android update sdk -u -a --filter android-21 && \
    echo "y" | android update sdk -u -a --filter build-tools-21.1.2 && \
    echo "y" | android update sdk -u -a --filter build-tools-21.1.1 && \
    echo "y" | android update sdk -u -a --filter build-tools-21.1.0 && \
    echo "y" | android update sdk -u -a --filter build-tools-21.0.2 && \
    echo "y" | android update sdk -u -a --filter build-tools-21.0.1 && \
    echo "y" | android update sdk -u -a --filter build-tools-21.0.0 && \
    echo "y" | android update sdk -u -a --filter android-20 && \
    echo "y" | android update sdk -u -a --filter build-tools-20.0.0 && \
    echo "y" | android update sdk -u -a --filter android-19 && \
    echo "y" | android update sdk -u -a --filter build-tools-19.1.0 && \
    echo "y" | android update sdk -u -a --filter build-tools-19.0.3 && \
    echo "y" | android update sdk -u -a --filter build-tools-19.0.2 && \
    echo "y" | android update sdk -u -a --filter build-tools-19.0.1

# Install React Native
RUN npm install -g react-native-cli

