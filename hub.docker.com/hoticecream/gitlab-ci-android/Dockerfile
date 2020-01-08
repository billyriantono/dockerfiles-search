FROM openjdk:8-jdk

ADD ssh /root/.ssh

RUN apt-get -y update

ENV ANDROID_HOME "/sdk"
ENV PATH "$PATH:${ANDROID_HOME}/tools"
ENV DEBIAN_FRONTEND noninteractive

ENV SDK_PACKAGES "\
tools,\
platform-tools,\
build-tools-25,\
build-tools-25.0.1,\
build-tools-25.0.2,\
android-25,\
android-24,\
addon-google_apis-google-25,\
platform-tools,\
extra-android-m2repository,\
extra-android-support,\
extra-google-google_play_services,\
extra-google-m2repository"


# Constraint Layout / [Solver for ConstraintLayout 1.0.0-alpha8, ConstraintLayout for Android 1.0.0-alpha8]
RUN mkdir -p $ANDROID_HOME/licenses/ && \
    echo "8933bad161af4178b1185d1a37fbf41ea5269c55" > $ANDROID_HOME/licenses/android-sdk-license && \
    echo "84831b9409646a918e30573bab4c9c91346d8abd" > $ANDROID_HOME/licenses/android-sdk-preview-license

ADD http://dl.google.com/android/repository/tools_r25.2.2-linux.zip /tools.zip

RUN unzip /tools.zip -d $ANDROID_HOME && \
    rm -v /tools.zip

RUN echo y | ${ANDROID_HOME}/tools/android update sdk -u -a -t ${SDK_PACKAGES}

RUN chmod 666 /root/.ssh/*