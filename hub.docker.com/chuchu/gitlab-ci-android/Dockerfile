#
# GitLab CI: Android v0.2
#
# https://hub.docker.com/r/jangrewe/gitlab-ci-android/
# https://git.faked.org/jan/gitlab-ci-android
#


FROM ubuntu:16.04
MAINTAINER achu <82724824@qq.com>

RUN dpkg-reconfigure locales

ENV VERSION_SDK_TOOLS "25.1.7"
ENV VERSION_BUILD_TOOLS "24.0.0"
ENV VERSION_TARGET_SDK "24"

ENV LANG "en_US.UTF-8"
ENV LC_COLLATE "en_US.UTF-8"
ENV LC_CTYPE "en_US.UTF-8"
ENV LC_MESSAGES "en_US.UTF-8"
ENV LC_MONETARY "en_US.UTF-8"
ENV LC_NUMERIC "en_US.UTF-8"
ENV LC_TIME "en_US.UTF-8"
ENV LC_ALL "en_US.UTF-8"

ENV SDK_PACKAGES "build-tools-${VERSION_BUILD_TOOLS},android-${VERSION_TARGET_SDK},addon-google_apis-google-${VERSION_TARGET_SDK},platform-tools,extra-android-m2repository,extra-android-support,extra-google-google_play_services,extra-google-m2repository"

ENV ANDROID_HOME "/sdk"
ENV ANDROID_NDK_HOME "/ndk"

ENV PATH "$PATH:${ANDROID_HOME}/tools:${ANDROID_NDK_HOME}"
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -qq update && \
    apt-get install -qqy --no-install-recommends \
      curl \
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

ADD http://dl.google.com/android/repository/tools_r${VERSION_SDK_TOOLS}-linux.zip /tools.zip
ADD http://dl.google.com/android/repository/android-ndk-r12b-linux-x86_64.zip     /ndk.zip
RUN unzip /tools.zip -d /sdk && \
    rm -v /tools.zip
RUN unzip /ndk.zip -d /ndk && \
    rm -v /ndk.zip

RUN (while [ 1 ]; do sleep 5; echo y; done) | ${ANDROID_HOME}/tools/android update sdk -u -a -t ${SDK_PACKAGES}
