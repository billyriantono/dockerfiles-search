FROM ubuntu:16.04

RUN apt-get update && apt-get install -y wget unzip make file
RUN wget https://dl.google.com/android/repository/android-ndk-r14b-linux-x86_64.zip && unzip android-ndk-r14b-linux-x86_64.zip
ENV ANDROID_NDK_HOME /android-ndk-r14b
CMD /android-ndk-r14b/ndk-build


