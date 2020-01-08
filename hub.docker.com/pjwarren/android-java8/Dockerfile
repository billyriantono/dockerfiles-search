# based on https://registry.hub.docker.com/u/samtstern/android-sdk/dockerfile/ with openjdk-8
FROM openjdk:8

MAINTAINER Phillip Warren <phillip.warren@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -yq libc6:i386 libstdc++6:i386 zlib1g:i386 libncurses5:i386 --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

# Download and unzip SDK
# At the time of writing, the latest file for the command line tools is
# referenced from this url: https://developer.android.com/studio/index.html#downloads

ARG ANDROID_SDK_URL=https://dl.google.com/android/repository/tools_r25.2.3-linux.zip
ARG ANDROID_SDK_CHECKSUM=aafe7f28ac51549784efc2f3bdfc620be8a08213

# Download archive, verify checksum, extract it, and finally remove archive
RUN curl -O $ANDROID_SDK_URL && \
    (BASENAME=`basename $ANDROID_SDK_URL`; \
    echo "${ANDROID_SDK_CHECKSUM} *${BASENAME}" | sha1sum --strict -c - && \
    unzip -q $BASENAME -d /usr/local/android-sdk-linux && \
    rm $BASENAME)
 
ENV ANDROID_HOME /usr/local/android-sdk-linux 
ENV ANDROID_SDK /usr/local/android-sdk-linux
ENV PATH ${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

# Install Android SDK packages
# See https://developer.android.com/studio/intro/update.html
# for information on which packages are necessary
# look at the output from the command
# $ANDROID_HOME/tools/android list sdk --extended --all --no-ui
# To find out what the package names are.
ARG ANDROID_PACKAGES="\
	tools,\
	platform-tools,\
	build-tools-25.0.1,\
	android-25,\
	extra-android-m2repository,\
	extra-google-m2repository"

# The while loop accepts each license
RUN ( while [ 1 ]; do sleep 5; echo y; done ) | \
    android update sdk --no-ui --all --filter "${ANDROID_PACKAGES}" && \
	rm -rf "${ANDROID_HOME}/temp"

# For gradle
ENV TERM dumb

# We don't install gradle here.
# Instead, the project repository contains the "gradle wrapper"
# Which automatically downloads the correct version of gradle

# Load licenses
COPY licenses $ANDROID_HOME/licenses
