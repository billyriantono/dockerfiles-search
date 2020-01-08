FROM alpine:3.7

ENV ANDROID_HOME /opt/android-sdk-linux
ENV GRADLE_HOME /opt/gradle

RUN mkdir -p GRADLE_HOME && mkdir -p ${ANDROID_HOME}

# install JDK and bash
RUN apk add --no-cache openjdk8 bash
# RUN DEBIAN_FRONTEND=noninteractive apt-get install -y openjdk-8-jdk

# Download Android SDK tools
RUN cd /opt \
    && wget -q https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -O android-sdk-tools.zip \
    && unzip -q android-sdk-tools.zip -d ${ANDROID_HOME} \
    && rm android-sdk-tools.zip

ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

# Accept licenses before installing components, no need to echo y for each component
# License is valid for all the standard components in versions installed from this file
# Non-standard components: MIPS system images, preview versions, GDK (Google Glass) and Android Google TV require separate licenses, not accepted there
RUN yes | sdkmanager  --licenses

RUN touch /root/.android/repositories.cfg

# Platform tools
RUN sdkmanager "tools" "platform-tools"

RUN yes | sdkmanager --update --channel=3

RUN yes | sdkmanager \
    "platforms;android-29" \
    "platforms;android-28" \
    "build-tools;28.0.3" \
    "extras;android;m2repository" \
    "extras;google;m2repository" \
    "extras;google;google_play_services"

# install gradle
ENV GRADLE_VERSION 5.4.1
RUN set -o errexit -o nounset \
    && echo "Downloading Gradle" \
    && wget --no-verbose --output-document=gradle.zip "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" \
    && echo "Installing Gradle" \
    && unzip gradle.zip \
    && rm gradle.zip \
    && mv "gradle-${GRADLE_VERSION}" "${GRADLE_HOME}/"

ENV PATH ${PATH}:${GRADLE_HOME}/bin
