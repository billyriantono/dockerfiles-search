FROM ubuntu:16.04

# Install JAVA 8.
RUN apt-get update -y && \
  apt-get install -y software-properties-common && \ 
  apt-add-repository ppa:webupd8team/java && \
  apt-get update -y && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
  apt-get install -y oracle-java8-installer && \
  apt-get install -y oracle-java8-unlimited-jce-policy && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
RUN echo $JAVA_HOME

# Install Deps
RUN dpkg --add-architecture i386 && apt-get update && apt-get install -y --force-yes expect unzip git wget libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libbz2-1.0:i386 python curl libqt5widgets5 && apt-get clean && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*


# Copy install tools
COPY tools /opt/tools
ENV PATH ${PATH}:/opt/tools

# Download and extract Android SDK Tools, Revision 26.0.2
RUN mkdir /opt/android-sdk-linux && \
    cd /opt/android-sdk-linux && \
    wget --output-document=android-sdk.zip --quiet https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip && \
    unzip android-sdk.zip && \
    rm -f android-sdk.zip && \
    chown -R root.root tools

# Set Android environtments
ENV ANDROID_HOME /opt/android-sdk-linux
ENV ANDROID_SDK_DIR /opt/android-sdk-linux
ENV ANDROID_SDK_HOME /opt/android-sdk-linux

# Accept all Android SDK licenses
RUN yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses

# Download Android development tools
RUN $ANDROID_HOME/tools/bin/sdkmanager "platform-tools"
RUN $ANDROID_HOME/tools/bin/sdkmanager "build-tools;27.0.3"
RUN $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-27"
RUN $ANDROID_HOME/tools/bin/sdkmanager "extras;android;m2repository"
RUN $ANDROID_HOME/tools/bin/sdkmanager "extras;google;m2repository"
RUN $ANDROID_HOME/tools/bin/sdkmanager "extras;google;google_play_services"
RUN $ANDROID_HOME/tools/bin/sdkmanager "add-ons;addon-google_apis-google-24"
RUN $ANDROID_HOME/tools/bin/sdkmanager "system-images;android-24;google_apis;armeabi-v7a"


# Gradle install
RUN add-apt-repository ppa:cwchien/gradle
RUN apt-get update
RUN apt-get -y install gradle
RUN gradle -v

# Setup environment
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools

# Check adb and android
RUN which adb
RUN which android

# Create emulator
RUN $ANDROID_HOME/tools/bin/avdmanager create avd \
        --name test \
        --package 'system-images;android-24;google_apis;armeabi-v7a' \
        --tag "google_apis" \
        --abi "armeabi-v7a" \
        --device "Nexus 5" \
        --force

# Cleaning
RUN apt-get clean

# Go to workspace
RUN mkdir -p /opt/workspace
WORKDIR /opt/workspace
RUN touch /opt/android-sdk-linux/.android/emu-update-last-check.ini

