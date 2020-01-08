# ====================================================================== #
# Android SDK Docker Image
# ====================================================================== #

# Base image
# ---------------------------------------------------------------------- #
FROM circleci/android:api-28


# ====================================================================== #
# Setup Python 3.7
# ====================================================================== #
RUN sudo apt-get update \
    && sudo apt-get install -y software-properties-common build-essential sqlite3 libsqlite3-dev zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget \
    && sudo curl -O https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tar.xz \
    && sudo tar -xf Python-3.7.3.tar.xz \
    && cd Python-3.7.3 \
    && sudo ./configure --enable-optimizations \
    && sudo make -j 8 \
    && sudo make altinstall

# ====================================================================== #
# Update Android SDK
# ====================================================================== #

ENV PATH ${ANDROID_HOME}/emulator:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools/bin:${PATH}

RUN ${ANDROID_HOME}/tools/bin/sdkmanager --update
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "build-tools;28.0.3"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "platform-tools"
RUN ${ANDROID_HOME}/tools/bin/sdkmanager "emulator"
