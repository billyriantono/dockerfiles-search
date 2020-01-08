FROM java:8
MAINTAINER lhcpig <lhcpig@qq.com>

RUN apt-get update && apt-get install -y gcc-multilib lib32z1 && apt-get clean

ENV ANDROID_SDK_VERSION r26.0.2
WORKDIR /opt
RUN curl -sLO https://dl.google.com/android/android-sdk_${ANDROID_SDK_VERSION}-linux.tgz && \
  tar zxvf android-sdk_${ANDROID_SDK_VERSION}-linux.tgz && \
  ln -s android-sdk-linux android-sdk && \
  rm android-sdk_${ANDROID_SDK_VERSION}-linux.tgz

ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
 
ENV GRADLE_VERSION 4.1
WORKDIR /usr/bin
RUN curl -sLO https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip && \
  unzip gradle-${GRADLE_VERSION}-bin.zip && \
  ln -s gradle-${GRADLE_VERSION} gradle && \
  rm gradle-${GRADLE_VERSION}-bin.zip

ENV ANDROID_M2REPOSITORY_VERSION r26
ENV ANDROID_SUPPORT_VERSION r26.0.2
ENV ANDROID_PLATFORM_VERSION 26_r02
#ENV ANDROID_PLATFORM_TOOLS_VERSION r24.4.1
ENV ANDROID_BUILD_TOOLS_VERSION r26.0.2

RUN curl -sLO https://dl.google.com/android/repository/android-${ANDROID_PLATFORM_VERSION}.zip && \
  unzip android-${ANDROID_PLATFORM_VERSION}.zip -d ${ANDROID_HOME}/platforms&& \
  rm android-${ANDROID_PLATFORM_VERSION}.zip
  
RUN mkdir -p ${ANDROID_HOME}/extras/android
RUN curl -sLO https://dl.google.com/android/repository/android_m2repository_${ANDROID_M2REPOSITORY_VERSION}.zip && \
  unzip android_m2repository_${ANDROID_M2REPOSITORY_VERSION}.zip -d ${ANDROID_HOME}/extras/android&& \
  rm android_m2repository_${ANDROID_M2REPOSITORY_VERSION}.zip
  
RUN curl -sLO https://dl.google.com/android/repository/support_${ANDROID_SUPPORT_VERSION}.zip && \
  unzip support_${ANDROID_SUPPORT_VERSION}.zip -d ${ANDROID_HOME}/extras/android&& \
  rm support_${ANDROID_SUPPORT_VERSION}.zip
  
#RUN curl -sLO https://dl.google.com/android/repository/platform-tools_${ANDROID_PLATFORM_TOOLS_VERSION}-linux.zip && \
#  unzip platform-tools_${ANDROID_PLATFORM_TOOLS_VERSION}-linux.zip -d ${ANDROID_HOME} && \
#  rm platform-tools_${ANDROID_PLATFORM_TOOLS_VERSION}-linux.zip

RUN mkdir -p ${ANDROID_HOME}/build-tools
RUN curl -sLO https://dl.google.com/android/repository/build-tools_${ANDROID_BUILD_TOOLS_VERSION}-linux.zip && \
  unzip build-tools_${ANDROID_BUILD_TOOLS_VERSION}-linux.zip -d ${ANDROID_HOME}/build-tools && \
  rm build-tools_${ANDROID_BUILD_TOOLS_VERSION}-linux.zip

ENV GRADLE_HOME /usr/bin/gradle
ENV PATH $PATH:$GRADLE_HOME/bin

RUN mkdir /app
WORKDIR /app
CMD ["gradle", "build"]
