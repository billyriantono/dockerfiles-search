FROM ubuntu:latest

ENV ANDROID_HOME "/sdk"
ENV PATH "$PATH:${ANDROID_HOME}/tools"

RUN apt-get update
RUN apt-get install -qqy --no-install-recommends \
  openjdk-8-jdk \
  unzip
RUN apt-get clean

ADD packages.txt /
ADD https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip /tools.zip

RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN unzip /tools.zip -d ${ANDROID_HOME}
RUN rm -v /tools.zip
RUN mkdir -p /root/.android 
RUN touch /root/.android/repositories.cfg 
RUN ${ANDROID_HOME}/tools/bin/sdkmanager --update
RUN (while [ 1 ]; do sleep 5; echo y; done) | ${ANDROID_HOME}/tools/bin/sdkmanager --package_file=packages.txt
RUN yes | ${ANDROID_HOME}/tools/bin/sdkmanager --licenses
