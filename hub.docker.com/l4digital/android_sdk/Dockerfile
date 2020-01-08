FROM ubuntu:16.04

MAINTAINER Brett McGinnis brett@l4digital.com

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
    unzip \
    wget \
    default-jdk

ARG ANDROID_HOME=/opt/android-sdk

RUN wget https://dl.google.com/android/repository/tools_r25.2.3-linux.zip && \
    unzip tools_r25.2.3-linux.zip -d ${ANDROID_HOME}

# possible filters [add-on, doc, extra, platform, platform-tool, sample, source, system-image, tool]
RUN (while :; do   echo 'y';   sleep 1; done) | \
    ${ANDROID_HOME}/tools/android update sdk \
    --no-ui \
    --filter platform,platform-tool,system-image

# Running with out filter installs latest build tools
RUN (while :; do   echo 'y';   sleep 1; done) | \
    ${ANDROID_HOME}/tools/android update sdk \
    --no-ui

ENV ANDROID_HOME=${ANDROID_HOME}
ENV PATH=${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
