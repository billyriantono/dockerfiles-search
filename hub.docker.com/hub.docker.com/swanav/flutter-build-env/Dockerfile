FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
	curl \
	git \
	xz-utils \
	libglu1-mesa \
	wget \
	unzip \
	lib32stdc++6
RUN apt-get install -y openjdk-8-jdk

WORKDIR /development/android
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
RUN unzip sdk-tools-linux-4333796.zip

WORKDIR /development/android/tools/bin
# ENV JAVA_OPTS="-XX:+IgnoreUnrecognizedVMOptions --add-modules java.se.ee"
RUN yes | ./sdkmanager --install "platform-tools" "platforms;android-28" "build-tools;29.0.0"
ENV ANDROID_HOME="/development/android"
ENV PATH="${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${PATH}"

WORKDIR /development
RUN wget https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_v1.7.8+hotfix.4-stable.tar.xz
RUN tar xf flutter_linux_v1.7.8+hotfix.4-stable.tar.xz

ENV PATH="/development/flutter/bin:${PATH}"
RUN printenv PATH

RUN yes | flutter doctor --android-licenses
RUN flutter doctor

WORKDIR /app
