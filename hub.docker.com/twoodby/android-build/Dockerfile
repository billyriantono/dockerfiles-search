# Android Dockerfile

FROM ubuntu:16.10

# ------------------------------------------------------------------------------
# ENV Settings
# ------------------------------------------------------------------------------
ENV ANDROID_HOME /opt/android-sdk-linux
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [105MB]


# ------------------------------------------------------------------------------
# Setup Base System: Install System Tools
# ------------------------------------------------------------------------------
RUN apt-get update -qq &&  \
    apt-get install -y unzip && \
    apt-get clean
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [143MB]


# ------------------------------------------------------------------------------
# Install JAVA OpenJDK
# ------------------------------------------------------------------------------
ENV JAVA_OPENJDK_VERSION 8

RUN apt-get install -y openjdk-$JAVA_OPENJDK_VERSION-jdk wget expect && \
    apt-get clean
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [552MB]


# ------------------------------------------------------------------------------
# Install Android SDK Tools
# These will be used to update the SDKs and install other needed files.
# ------------------------------------------------------------------------------
ENV ANDROID_SDK_TOOLS_VERSION 25.1.7

RUN mkdir $ANDROID_HOME && \
    cd $ANDROID_HOME && \
    wget https://dl.google.com/android/repository/tools_r$ANDROID_SDK_TOOLS_VERSION-linux.zip -O android-sdk.zip && \
    unzip android-sdk.zip && \
    rm -f android-sdk.zip

ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [961MB]


# ------------------------------------------------------------------------------
# Install Android Platform-Tools (via android update sdk)
# ------------------------------------------------------------------------------
RUN echo y | android update sdk --no-ui --all --filter platform-tools | grep 'package installed'
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [998MB]


# ------------------------------------------------------------------------------
# Install SDKs
# ------------------------------------------------------------------------------
ENV ANDROID_SDK_VERSION_MIN 23
ENV ANDROID_SDK_VERSION_MAX 25

RUN echo y | android update sdk --no-ui --all --filter android-$ANDROID_SDK_VERSION_MAX | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter android-$ANDROID_SDK_VERSION_MIN | grep 'package installed'
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [1.23GB]


# ------------------------------------------------------------------------------
# Install Build Tools
# ------------------------------------------------------------------------------
ENV ANDROID_BUILD_TOOLS_VERSION_MIN 23.0.3
ENV ANDROID_BUILD_TOOLS_VERSION_MAX 25.0.2

RUN echo y | android update sdk --no-ui --all --filter build-tools-$ANDROID_BUILD_TOOLS_VERSION_MAX | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-$ANDROID_BUILD_TOOLS_VERSION_MIN | grep 'package installed'
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [1.45GB]


# ------------------------------------------------------------------------------
# Install Extras
# ------------------------------------------------------------------------------
RUN echo y | android update sdk --no-ui --all --filter extra-android-m2repository | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter extra-google-m2repository | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter extra-google-google_play_services | grep 'package installed'
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [2.06GB]


# ------------------------------------------------------------------------------
# Install NDK
# ------------------------------------------------------------------------------
ENV ANDROID_NDK_VERSION r12

RUN cd /usr/local && \
    wget https://dl.google.com/android/repository/android-ndk-$ANDROID_NDK_VERSION-linux-x86_64.zip -O android-ndk.zip && \
    unzip android-ndk.zip && \
    rm android-ndk.zip
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ [4.67GB]


# ------------------------------------------------------------------------------
# Setup ENV Variables
# ------------------------------------------------------------------------------

# Environment variables
# ENV ANDROID_HOME /usr/local/android-sdk
ENV ANDROID_SDK_HOME $ANDROID_HOME
ENV ANDROID_NDK_HOME /usr/local/android-ndk
ENV JENKINS_HOME $HOME
ENV PATH ${INFER_HOME}/bin:${PATH}
ENV PATH $PATH:$ANDROID_SDK_HOME/tools
ENV PATH $PATH:$ANDROID_SDK_HOME/platform-tools
ENV PATH $PATH:$ANDROID_SDK_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION_MIN
ENV PATH $PATH:$ANDROID_SDK_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION_MAX
ENV PATH $PATH:$ANDROID_NDK_HOME

# Export JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-$JAVA_OPENJDK_VERSION-openjdk-amd64/

# Support Gradle
ENV TERM dumb
ENV JAVA_OPTS "-Xms4096m -Xmx4096m"
ENV GRADLE_OPTS "-XX:+UseG1GC -XX:MaxGCPauseMillis=1000"


# # ------------------------------------------------------------------------------
# # Setup Build User
# # ------------------------------------------------------------------------------
#
# # Add build user account, values are set to default below
# ENV RUN_USER mobileci
# ENV RUN_UID 5089
#
# RUN id $RUN_USER || adduser --uid "$RUN_UID" \
#     --gecos 'Build User' \
#     --shell '/bin/sh' \
#     --disabled-login \
#     --disabled-password "$RUN_USER"
#
# # Fix permissions
# RUN chown -R $RUN_USER:$RUN_USER $ANDROID_HOME $ANDROID_SDK_HOME
# # $ANDROID_NDK_HOME
# RUN chmod -R a+rx $ANDROID_HOME $ANDROID_SDK_HOME
# # $ANDROID_NDK_HOME

COPY licenses ${ANDROID_HOME}/licenses


# Creating project directories prepared for build when running
# `docker run`
ENV PROJECT /project
RUN mkdir $PROJECT
# RUN chown -R $RUN_USER:$RUN_USER $PROJECT
WORKDIR $PROJECT

# USER $RUN_USER
# RUN echo "sdk.dir=$ANDROID_HOME" > local.properties
