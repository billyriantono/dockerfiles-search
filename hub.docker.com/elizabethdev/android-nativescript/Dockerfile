FROM ubuntu:latest
LABEL maintainer="Elizabeth Martín Campos <eli@zabeth.es>"

RUN useradd -ms /bin/bash nativescript

COPY docker-entrypoint.sh /docker-entrypoint.sh

# Utilities
RUN apt-get update && \
    apt-get -y install apt-transport-https curl unzip usbutils --no-install-recommends && \
    rm -r /var/lib/apt/lists/*

# NodeJS
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get update && \
    apt-get -y install nodejs npm --no-install-recommends && \
    rm -r /var/lib/apt/lists/*

# Android build requirements
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get -y install lib32z1 lib32ncurses5 libbz2-1.0:i386 libstdc++6:i386 g++ --no-install-recommends && \
    rm -r /var/lib/apt/lists/*

# JAVA
RUN apt-get update && \
    apt-get -y install software-properties-common && \
    add-apt-repository ppa:webupd8team/java && \
    apt-get update && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    apt-get -y install oracle-java8-installer --no-install-recommends && \
    export JAVA_HOME=$(update-alternatives --query javac | sed -n -e 's/Best: *\(.*\)\/bin\/javac/\1/p') && \
    rm -r /var/lib/apt/lists/*

# NativeScript
RUN npm install -g nativescript --unsafe-perm && \
    tns error-reporting disable

# Android SDK
ARG ANDROID_SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip"
ARG ANDROID_SYSTEM_PACKAGE="platforms;android-28"
ARG ANDROID_BUILD_TOOLS_PACKAGE="build-tools;28.0.3"
ARG ANDROID_PACKAGES="tools platform-tools $ANDROID_SYSTEM_PACKAGE $ANDROID_BUILD_TOOLS_PACKAGE extras;android;m2repository extras;google;m2repository"
ADD $ANDROID_SDK_URL /tmp/android-sdk.zip
RUN mkdir /opt/android-sdk /app /dist && \
    chown nativescript:nativescript /tmp/android-sdk.zip /opt/android-sdk /app /dist
USER nativescript
ENV ANDROID_HOME /opt/android-sdk
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools/bin
RUN tns error-reporting disable && \
    unzip -q /tmp/android-sdk.zip -d /opt/android-sdk && \
    rm /tmp/android-sdk.zip && \
    mkdir /home/nativescript/.android && \
    touch /home/nativescript/.android/repositories.cfg && \
    yes | /opt/android-sdk/tools/bin/sdkmanager --licenses && \
    /opt/android-sdk/tools/bin/sdkmanager --update && \
    echo "y" | /opt/android-sdk/tools/bin/sdkmanager $ANDROID_PACKAGES
# Self-update of 'tools' package is currently not working?
#RUN echo "y" | /opt/android-sdk/tools/android --silent update sdk -a -u -t tools

VOLUME ["/app","/dist"]

WORKDIR /app

CMD ["/docker-entrypoint.sh"]
