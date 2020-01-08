# ====================================================================== #
# Android SDK Docker Image
# ====================================================================== #

# Base image
# ---------------------------------------------------------------------- #
FROM thyrlian/android-sdk


# ====================================================================== #
# Setup Python 3.7
# ====================================================================== #
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:jonathonf/python-3.7 -y
RUN apt-get update -y
RUN apt-get install -y build-essential sqlite3 libsqlite3-dev python3.7 python3.7-dev python3-pip python3.7-venv


# ====================================================================== #
# Update Android SDK
# ====================================================================== #

RUN mkdir -p /sdk

# ANDROID_HOME is /opt/android-sdk from thyrlian/android-sdk image
RUN cp -a $ANDROID_HOME/. /sdk
RUN chmod 777 -R /sdk

# now set it to /sdk
ENV ANDROID_HOME /sdk
# todo, fix why path still picks up /sdk/tools/emulator not the sdk/emulator/emulator
ENV PATH ${ANDROID_HOME}/emulator/emulator:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools/bin:${PATH}

RUN ${ANDROID_HOME}/tools/bin/sdkmanager --update
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "build-tools;28.0.3"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "platform-tools"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "emulator"

