# build with `docker build . -t narfman0/docker-android-sdk`
FROM openjdk:8-jdk

# Set desired Android Linux SDK version
ENV ANDROID_SDK_ZIP_URL https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip
ENV ANDROID_HOME /opt/android-sdk
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools

USER root

# dependencies for setup process
RUN dpkg --add-architecture i386
RUN apt-get update && \
    apt-get install -y software-properties-common unzip \
    libc6:i386 libncurses5:i386 libstdc++6:i386 zlib1g:i386 # 32bit compatibility

# install android sdk
RUN mkdir -p $ANDROID_HOME
ADD $ANDROID_SDK_ZIP_URL $ANDROID_HOME
RUN cd $ANDROID_HOME && \
    unzip *tools*linux*.zip && \
    rm *tools*linux*.zip
