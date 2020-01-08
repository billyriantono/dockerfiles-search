FROM java:7-jdk

MAINTAINER Benjamin Böhmke

# get dependencies for android SDK
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -yq zip rsync libc6:i386 libstdc++6:i386 zlib1g:i386 libncurses5:i386 --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# get and install gradle and android SDK
RUN curl -sSL https://services.gradle.org/distributions/gradle-2.11-bin.zip -o /tmp/gradle-bin.zip && \
    curl -sSL http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz | tar xz -C /usr/local && \
    unzip /tmp/gradle-bin.zip -d /usr/local && \
    rm /tmp/*

# define android SDK components
ENV ANDROID_SDK_COMPONENTS \
    platform-tools,build-tools-22.0.1,build-tools-23.0.1,android-23,extra-android-support,\
    addon-google_apis-google-23,extra-google-google_play_services,\
    extra-android-m2repository,extra-google-m2repository,extra-google-play_apk_expansion,\
    build-tools-23.0.2

# define android home
ENV ANDROID_HOME /usr/local/android-sdk-linux

# install SDK components
RUN echo y | ${ANDROID_HOME}/tools/android update sdk --no-ui --all --filter "${ANDROID_SDK_COMPONENTS}"

# set path
ENV PATH $PATH:${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:/usr/local/gradle-2.11/bin

# add volume for source code
VOLUME /src/
WORKDIR /src/
