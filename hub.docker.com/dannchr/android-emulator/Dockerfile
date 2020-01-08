FROM dannchr/android-build

# Script to be called to be sure emulator is running before starting to use it.
COPY ./android-wait-for-emulator /scripts/
ENV PATH /scripts:${PATH}

RUN sdkmanager --list --verbose

# Install Android SDK Tools (including avdmanager)
RUN echo y | sdkmanager \
    "tools"

# Import some emulator images.
RUN echo y | sdkmanager \
    "system-images;android-22;google_apis;armeabi-v7a"

ENV PATH ${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools:${PATH}

RUN echo $PATH
RUN ls -lR $ANDROID_HOME

RUN sdkmanager --list

# Define some emulator machines based on the emulator images.
RUN echo no | avdmanager \
    create avd --name test22 \
               --package 'system-images;android-22;google_apis;armeabi-v7a' \
               --abi 'google_apis/armeabi-v7a'

