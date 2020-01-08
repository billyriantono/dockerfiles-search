FROM openjdk:8-jdk
LABEL maintainer="boxresin@gmail.com"

# Install Android SDK
RUN wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip && \
    mkdir /opt/android-sdk-linux && \
    unzip -qq android-sdk.zip -d /opt/android-sdk-linux && \
    rm -f android-sdk.zip

# Set environment variables
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH $PATH:$ANDROID_HOME/platform-tools/

# Make repositories.cfg
RUN mkdir $ANDROID_SDK_HOME/.android && \
    echo 'count=0' > $ANDROID_SDK_HOME/.android/repositories.cfg

# Install components
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager --licenses && \
    echo y | $ANDROID_HOME/tools/bin/sdkmanager --update && \
    echo y | $ANDROID_HOME/tools/bin/sdkmanager "extras;google;m2repository" "extras;android;m2repository"
