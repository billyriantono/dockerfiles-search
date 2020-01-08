FROM zbjumper/ci-base-gradle:2.14.1

MAINTAINER zbjumper <zbjumper@126.com>

ENV DEBIAN_FRONTEND noninteractive

ENV ANDROID_HOME "${SDK_HOME}/android_sdk"
ENV PATH "$PATH:${ANDROID_HOME}/tools"

ENV VERSION_SDK_TOOLS "25.2.2"
ENV VERSION_BUILD_TOOLS "23.0.3"
ENV VERSION_TARGET_SDK "23"

ENV SDK_PACKAGES "build-tools-${VERSION_BUILD_TOOLS},android-22,android-23,addon-google_apis-google-${VERSION_TARGET_SDK},platform-tools,extra-android-m2repository,extra-android-support,extra-google-google_play_services,extra-google-m2repository"


# Constraint Layout / [Solver for ConstraintLayout 1.0.0-alpha8, ConstraintLayout for Android 1.0.0-alpha8]
RUN mkdir -p $ANDROID_HOME/licenses/
RUN echo "8933bad161af4178b1185d1a37fbf41ea5269c55" > $ANDROID_HOME/licenses/android-sdk-license

RUN rm -f /etc/ssl/certs/java/cacerts; \
    /var/lib/dpkg/info/ca-certificates-java.postinst configure

ADD http://dl.google.com/android/repository/tools_r${VERSION_SDK_TOOLS}-linux.zip /tools.zip
RUN unzip /tools.zip -d ${ANDROID_HOME} && \
    rm -v /tools.zip

RUN (while [ 1 ]; do sleep 5; echo y; done) | ${ANDROID_HOME}/tools/android update sdk -u -a -t ${SDK_PACKAGES}


