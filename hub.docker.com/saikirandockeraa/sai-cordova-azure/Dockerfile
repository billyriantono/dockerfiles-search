FROM circleci/android:api-28-node8-alpha

MAINTAINER Sai K Tagore <kiran3047@gmail.com>

# Update Android SDK
RUN yes | sdkmanager --licenses
RUN yes | sdkmanager "build-tools;28.0.3"
RUN yes | sdkmanager "platforms;android-28"
RUN yes | sdkmanager "platform-tools"
RUN yes | sdkmanager "tools"

# Install Cordova and Ionic
RUN sudo npm update -g
RUN sudo npm install -g ionic@3.2.0 cordova@8.0.0
RUN cordova telemetry off
RUN CI=true ionic config set -g daemon.updates false
RUN ionic config set -g telemetry false

#Install increase-memory-limit
RUN sudo  npm i -g increase-memory-limit
RUN sudo increase-memory-limit

# Install Fastlane
RUN gem install fastlane -NV

# Install Gradle
ARG GRADLE_VERSION=4.8.1
RUN sudo curl https://downloads.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip > /tmp/gradle-$GRADLE_VERSION-bin.zip
RUN sudo unzip /tmp/gradle-$GRADLE_VERSION-bin.zip -d /tmp && rm /tmp/gradle-$GRADLE_VERSION-bin.zip
RUN sudo mv /tmp/gradle-$GRADLE_VERSION /opt/gradle
ENV PATH="/opt/gradle/bin:${PATH}"

CMD /bin/sh
