FROM scalac/java8:latest

MAINTAINER Jakub Zubielik "jakub.zubielik@scalac.io"

ENV ANDROID_SDK_VERSION 24.4.1

RUN update-ca-certificates -f

RUN cd /opt && \
	  wget -O android-sdk.tgz https://dl.google.com/android/android-sdk_r$ANDROID_SDK_VERSION-linux.tgz && \
    tar zxf android-sdk.tgz && \
    rm -f android-sdk.tgz && \
    chown -R root:root android-sdk-linux

RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    apt-get install -y --force-yes expect git lib32z1 libc6:i386 libncurses5:i386 libstdc++6:i386

ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

RUN echo '#!/usr/bin/expect -f\n\
set timeout 3600\n\
set filter [lindex $argv 0]\n\
spawn android update sdk --all --force --no-ui --filter $filter\n\
expect {\n\
  "Do you accept the license *" {\n\
        exp_send "y\r"\n\
        exp_continue\n\
  }\n\
  eof\n\
}' \
> /opt/android-sdk-linux/install-headless.sh

RUN chmod +x /opt/android-sdk-linux/install-headless.sh

ENV ANDROID_SDK_PACKAGES addon-google_apis_x86-google-21,android-21,android-22,android-23,build-tools-21,build-tools-21.0.1,build-tools-21.0.2,build-tools-21.1,build-tools-21.1.1,build-tools-21.1.2,build-tools-22,build-tools-22.0.1,build-tools-23.0.2,extra-android-m2repository,extra-android-support,extra-google-google_play_services,extra-google-m2repository,platform-tools,tools

RUN /opt/android-sdk-linux/install-headless.sh $ANDROID_SDK_PACKAGES

RUN rm -rf /var/lib/apt/lists/* && \
    apt-get autoremove -y && \
    apt-get clean

