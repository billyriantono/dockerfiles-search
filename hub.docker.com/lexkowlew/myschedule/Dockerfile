FROM java:8

MAINTAINER Leviz <alexleviz13@gmail.com>

# Install dependencies
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -yq libstdc++6:i386 zlib1g:i386 libncurses5:i386 --no-install-recommends && \
    apt-get -y install --reinstall locales && \
    dpkg-reconfigure locales && \
    echo 'ja_JP.UTF-8 UTF-8' >> /etc/locale.gen && \
    locale-gen ja_JP.UTF-8 && \
    localedef --list-archive && locale -a &&  \
    update-locale &&  \
    apt-get clean

# Download and untar SDK
ENV ANDROID_SDK_URL http://dl.google.com/android/android-sdk_r24.2-linux.tgz
RUN curl -L "${ANDROID_SDK_URL}" | tar --no-same-owner -xz -C /usr/local
ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANDROID_SDK /usr/local/android-sdk-linux
ENV PATH ${ANDROID_HOME}/tools:$ANDROID_HOME/platform-tools:$PATH

# Install Android SDK components

COPY android_sdk_components.env /android_sdk_components.env
RUN (while :; do echo 'y'; sleep 3; done) | android update sdk --no-ui --all --filter "$(cat /android_sdk_components.env)"

# Support Gradle
ENV TERM dumb
ENV JAVA_OPTS -Xms256m -Xmx512m

ENV PROJECT /project
RUN mkdir $PROJECT
WORKDIR $PROJECT
COPY . $PROJECT
RUN chmod +x gradlew
RUN echo "sdk.dir=$ANDROID_HOME" > local.properties
RUN ./gradlew --stacktrace androidDependencies
CMD ./gradlew --stacktrace build