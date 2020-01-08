FROM gradle:5.5.0-jdk8
RUN wget -q -O /tmp/sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip && \
  unzip /tmp/sdk.zip -d /opt/android-sdk && \
  rm /tmp/sdk.zip
RUN echo y | /opt/android-sdk/tools/bin/sdkmanager "platforms;android-28" "build-tools;28.0.3"
ENV ANDROID_HOME=/opt/android-sdk
