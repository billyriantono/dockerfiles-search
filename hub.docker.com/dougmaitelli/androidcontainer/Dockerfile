FROM openjdk:latest

# Download and untar SDK
ENV ANDROID_SDK_URL https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip
WORKDIR /usr/local
RUN curl -L "${ANDROID_SDK_URL}" > tools.zip && unzip tools.zip && rm tools.zip
ENV ANDROID_HOME /usr/local/tools
ENV ANDROID_SDK /usr/local/tools
ENV PATH ${ANDROID_HOME}:${ANDROID_HOME}/bin:$PATH

# Install Android SDK components
RUN yes | sdkmanager --licenses
RUN sdkmanager "build-tools;26.0.2" "platform-tools" "tools" "platforms;android-26" "extras;android;m2repository" "extras;google;m2repository"
