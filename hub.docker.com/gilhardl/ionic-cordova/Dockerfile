FROM gilhardl/ionic

LABEL author="Lucas GILHARD <l.gilhard@gmail.com>"
LABEL description="Docker image for Ionic Cordova development"

WORKDIR /usr/src/app/

USER root

# ENVIRONNEMENT
ENV GLIB_PACKAGE_BASE_URL https://github.com/sgerrand/alpine-pkg-glibc/releases/download
ENV GLIB_VERSION 2.29-r0

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk

ENV GRADLE_HOME /usr/local/gradle
ENV GRADLE_VERSION 4.4

ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANDRDOID_TOOLS_VERSION r25.2.5
ENV ANDROID_API_LEVELS android-26
ENV ANDROID_BUILD_TOOLS_VERSION 26.0.2

ENV PATH ${GRADLE_HOME}/bin:${JAVA_HOME}/bin:${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

RUN apk add --no-cache nss

# JAVA
RUN apk update && \
  apk add openjdk8-jre openjdk8

# GRADLE
RUN mkdir -p ${GRADLE_HOME} && \
  curl -L https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip > /tmp/gradle.zip && \
  unzip /tmp/gradle.zip -d ${GRADLE_HOME} && \
  mv ${GRADLE_HOME}/gradle-${GRADLE_VERSION}/* ${GRADLE_HOME} && \
  rm -r ${GRADLE_HOME}/gradle-${GRADLE_VERSION}/

# GLIBC
RUN curl -L https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r2/sgerrand.rsa.pub > /etc/apk/keys/sgerrand.rsa.pub && \
  curl -L ${GLIB_PACKAGE_BASE_URL}/${GLIB_VERSION}/glibc-${GLIB_VERSION}.apk > /tmp/glibc.apk && \
  curl -L ${GLIB_PACKAGE_BASE_URL}/${GLIB_VERSION}/glibc-bin-${GLIB_VERSION}.apk > /tmp/glibc-bin.apk && \
  apk add /tmp/glibc-bin.apk /tmp/glibc.apk

# ANDROID
RUN mkdir -p ${ANDROID_HOME} && \
  curl -L https://dl.google.com/android/repository/tools_${ANDRDOID_TOOLS_VERSION}-linux.zip > /tmp/tools.zip && \
  unzip /tmp/tools.zip -d ${ANDROID_HOME}

# ANDROID SDK
RUN echo y | android update sdk --no-ui -a --filter platform-tools,${ANDROID_API_LEVELS},build-tools-${ANDROID_BUILD_TOOLS_VERSION}

# CORDOVA
RUN npm install -g cordova

# CLEAN UP
RUN rm -rf /tmp/* /var/cache/apk/*

CMD ["bash"]