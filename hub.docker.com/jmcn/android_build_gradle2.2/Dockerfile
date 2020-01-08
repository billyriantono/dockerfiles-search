FROM java:jdk

ENV DEBIAN_FRONTEND noninteractive

# Dependencies
RUN dpkg --add-architecture i386 && apt-get update && apt-get install -yq libstdc++6:i386 zlib1g:i386 libncurses5:i386 ant maven --no-install-recommends
ENV GRADLE_URL http://services.gradle.org/distributions/gradle-2.2-all.zip
RUN curl -L ${GRADLE_URL} -o /tmp/gradle-2.2-all.zip && unzip /tmp/gradle-2.2-all.zip -d /usr/local && rm /tmp/gradle-2.2-all.zip
ENV GRADLE_HOME /usr/local/gradle-2.2
ENV PATH ${GRADLE_HOME}/bin:$PATH

# Download and untar SDK
ENV ANDROID_SDK_URL http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
RUN curl -L ${ANDROID_SDK_URL} | tar xz -C /usr/local
ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANDROID_SDK ${SDK_HOME}/android-sdk-linux
ENV PATH ${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

# Install Android SDK components
ENV ANDROID_COMPONENTS platform-tools,build-tools-19.1.0,android-19,build-tools-21.1.2,android-21,build-tools-22.0.1,android-22,build-tools-23.0.3,android-23,build-tools-24.0.2,android-24,extra
ENV GOOGLE_COMPONENTS extra-android-m2repository,extra-google-m2repository
RUN echo y | android update sdk --no-ui --all --filter ${ANDROID_COMPONENTS} ; \
    echo y | android update sdk --no-ui --all --filter ${GOOGLE_COMPONENTS}