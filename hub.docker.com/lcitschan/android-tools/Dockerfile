FROM lcitschan/openjdk8

MAINTAINER lcitschan <ctairong@gmail.com>

ARG ANDROID_TOOLS=http://dl.google.com/android/repository/sdk-tools-linux-3859397.zip

ENV ANDROID_HOME /opt/android-sdk-linux

RUN DEBIAN_FRONTEND=noninteractive && \
	apt-get -q update && \
    apt-get install -q -y wget unzip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget -q -O tools.zip ${ANDROID_TOOLS} && \
	unzip -qq tools.zip -d $ANDROID_HOME && \
	rm tools.zip

RUN yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses