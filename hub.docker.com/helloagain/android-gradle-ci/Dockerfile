######################   Docker image for building android apps   ######################
########################################################################################
## META
## Version: 1.1
## Date: 2017-10-22
## Info: Heavly influenced from 'https://hub.docker.com/r/beevelop/android/~/dockerfile/'

# Build on ubuntu/xenial
FROM ubuntu:xenial
MAINTAINER eusebius90

# Setup environment variables
    # Basic ubuntu non-interactive settings
ENV DEBIAN_FRONTEND=noninteractive \
    TERM=xterm \
    # Setup Android SDK stuff
    # i.e. - where to download the sdk
    #      - the checksum of the downloaded file
    #      - the version of the build-tools that will be installed
    #      - the versions of android sdk that will be installed
    ANDROID_SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip" \
    ANDROID_SDK_FILE_CHECKSUM="444e22ce8ca0f67353bda4b85175ed3731cae3ffa695ca18119cbacef1c1bea0" \
    ANDROID_INSTALL_STRING="build-tools;26.0.2 \
                            extras;android;m2repository \
                            platforms;android-19 \
                            platforms;android-20 \
                            platforms;android-21 \
                            platforms;android-22 \
                            platforms;android-23 \
                            platforms;android-24 \
                            platforms;android-25 \
                            platforms;android-26" \
    # Setup Home folders
    JAVA_HOME=/usr/lib/jvm/java-8-oracle \
    ANT_HOME="/usr/share/ant" \
    MAVEN_HOME="/usr/share/maven" \
    GRADLE_HOME="/usr/share/gradle" \
    ANDROID_HOME="/opt/android"

# Install all updates and install dependencies (and finally clean up)
    # Update and install most basic stuff
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
      # Useful stuff for me
      aptitude \
      # Used for oracle-java-installer
      software-properties-common \
      # Android SDK stuff
      wget curl maven ant gradle libncurses5 libstdc++6 zlib1g && \

    # Install Java v8
    add-apt-repository ppa:webupd8team/java -y && \
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get update -y && \
    apt-get install -y oracle-java8-installer && \
    apt-get install -y oracle-java8-set-default && \

    # Cleanup
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV ANDROID_PACKAGES=
# Get and setup Android SDK
RUN cd /opt && \
    mkdir -p android && cd android && \
    wget -O tools.zip ${ANDROID_SDK_URL} && \
    if [ "$(sha256sum tools.zip | awk '{print $1}')" != "$ANDROID_SDK_FILE_CHECKSUM" ]; then exit 1; fi && \
    unzip tools.zip && rm tools.zip && \
    yes | ./tools/bin/sdkmanager --update && \
    yes | ./tools/bin/sdkmanager --licenses && \
    PROCESSED_ANDROID_APIS=$(echo "$ANDROID_INSTALL_STRING" | awk '$1=$1') && \
    ./tools/bin/sdkmanager $PROCESSED_ANDROID_APIS && \
    chmod a+x -R $ANDROID_HOME && \
    chown -R root:root $ANDROID_HOME
