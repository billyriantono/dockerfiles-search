#
# GitLab CI: Android
# Version: 1.0.0
#
# https://hub.docker.com/r/mightymalakai33/gitlab-ci-bowling-stats-docker/
#

FROM ubuntu:18.04
MAINTAINER Andrew Auclair <mightymalakai33@gmail.com>

ENV VERSION_SDK_TOOLS "4333796"
ENV GRADLE_VERSION "5.1.1"

ENV ANDROID_HOME "/sdk"
ENV GRADLE_HOME "/gradle"

ENV PATH "$PATH:${ANDROID_HOME}/tools:${GRADLE_HOME}/bin"
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -qq update && \
    apt-get install -qqy --no-install-recommends \
      bzip2 \
      curl \
      git-core \
      html2text \
      openjdk-8-jdk \
      libc6-i386 \
      lib32stdc++6 \
      lib32gcc1 \
      lib32ncurses5 \
      lib32z1 \
      unzip \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN rm -f /etc/ssl/certs/java/cacerts; \
    /var/lib/dpkg/info/ca-certificates-java.postinst configure

RUN curl -s https://dl.google.com/android/repository/sdk-tools-linux-${VERSION_SDK_TOOLS}.zip > /sdk.zip && \
    unzip /sdk.zip -d /sdk && \
    rm -v /sdk.zip

#RUN mkdir -p $ANDROID_HOME/licenses/ \
#  && echo "8933bad161af4178b1185d1a37fbf41ea5269c55\nd56f5187479451eabf01fb78af6dfcb131a6481e" > $ANDROID_HOME/licenses/android-sdk-license \
#  && echo "84831b9409646a918e30573bab4c9c91346d8abd" > $ANDROID_HOME/licenses/android-sdk-preview-license

# Accept licenses before installing components, no need to echo y for each component
# License is valid for all the standard components in versions installed from this file
# Non-standard components: MIPS system images, preview versions, GDK (Google Glass) and Android Google TV require separate licenses, not accepted there
RUN yes | ${ANDROID_HOME}/tools/bin/sdkmanager --licenses

# Platform tools
# RUN sdkmanager "emulator" "tools" "platform-tools"
    
ADD packages.txt /sdk
RUN mkdir -p /root/.android && \
  touch /root/.android/repositories.cfg && \
  ${ANDROID_HOME}/tools/bin/sdkmanager --update 

RUN yes | while read -r package; do PACKAGES="${PACKAGES}${package} "; done < /sdk/packages.txt && \
    ${ANDROID_HOME}/tools/bin/sdkmanager ${PACKAGES}
    
RUN curl -s -S -L https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip > /gradle.zip && \
    unzip /gradle.zip -d /gradle && \
    rm -v /gradle.zip
   
   
