#
# GitLab CI: Android v0.2
#
# https://hub.docker.com/r/showcheap/gitlab-ci-android/
#

FROM ubuntu:17.04
MAINTAINER Sucipto <chip@pringstudio.com>

ENV VERSION_SDK_TOOLS "3859397"
ENV VERSION_BUILD_TOOLS "26.0.1"
ENV VERSION_TARGET_SDK "26"

ENV SDK_PACKAGES "build-tools-${VERSION_BUILD_TOOLS},android-${VERSION_TARGET_SDK},addon-google_apis-google-${VERSION_TARGET_SDK},platform-tools,extra-android-m2repository,extra-android-support,extra-google-google_play_services,extra-google-m2repository,sys-img-x86-android-${VERSION_TARGET_SDK},sys-img-x86-google_apis-${VERSION_TARGET_SDK}"

ENV ANDROID_HOME "/sdk"
ENV ANDROID_SDK_ROOT "/sdk"
ENV PATH "$PATH:${ANDROID_HOME}/tools"
ENV DEBIAN_FRONTEND noninteractive

# Accept License
RUN mkdir -p $ANDROID_HOME/licenses/
RUN echo "8933bad161af4178b1185d1a37fbf41ea5269c55" > $ANDROID_HOME/licenses/android-sdk-license

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
      qtbase5-dev \
      qtdeclarative5-dev \
      wget \
      qemu-kvm \
      build-essential \
      python2.7 \
      python2.7-dev \
      yamdi \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN rm -f /etc/ssl/certs/java/cacerts; \
    /var/lib/dpkg/info/ca-certificates-java.postinst configure

RUN wget -nv https://dl.google.com/android/repository/sdk-tools-linux-${VERSION_SDK_TOOLS}.zip && unzip sdk-tools-linux-${VERSION_SDK_TOOLS}.zip -d /sdk && \
    rm -v sdk-tools-linux-${VERSION_SDK_TOOLS}.zip

RUN wget -nv https://pypi.python.org/packages/1e/8e/40c71faa24e19dab555eeb25d6c07efbc503e98b0344f0b4c3131f59947f/vnc2flv-20100207.tar.gz && tar -zxvf vnc2flv-20100207.tar.gz && rm vnc2flv-20100207.tar.gz && \
    cd vnc2flv-20100207 && ln -s /usr/bin/python2.7 /usr/bin/python && python setup.py install

RUN mkdir ${ANDROID_HOME}/tools/keymaps && \
    touch ${ANDROID_HOME}/tools/keymaps/en-us

RUN mkdir /helpers

COPY wait-for-avd-boot.sh /helpers

RUN (while [ 1 ]; do sleep 5; echo y; done) | ${ANDROID_HOME}/tools/bin/sdkmanager --update --verbose
