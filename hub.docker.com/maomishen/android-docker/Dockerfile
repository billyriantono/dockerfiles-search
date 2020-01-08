FROM ubuntu:18.04

# default
RUN apt-get update ; \
    apt-get upgrade -y ; \
    apt-get install -y \
    curl \
    git \
    wget \
    zip \
    unzip \
    locales ;

RUN rm -rf /var/lib/apt/lists/* && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

# install fastlane
RUN apt-get update ; \
    apt-get install -y make ; \
    apt-get install -y libc6-dev ; \
    apt-get install -y g++ ; \
    apt-get install -y ruby ruby-dev ; \
    gem install fastlane -NV ;

# pip3
RUN apt-get update ; \
    apt-get install -y python3-pip ;

# nodejs
RUN apt-get update ; \
    curl -sL https://deb.nodesource.com/setup_8.x | bash - ; \
    apt-get install -y nodejs ;

# java
RUN apt-get install -y openjdk-8-jdk ;

# gradle
RUN wget https://services.gradle.org/distributions/gradle-5.1-bin.zip -P /tmp ; \
    unzip -d /gradle /tmp/gradle-5.1-bin.zip ;

ENV GRADLE_HOME=/gradle/gradle-5.1
ENV PATH=${GRADLE_HOME}/bin:${PATH}

# android sdk manager
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -P /tmp; \
    unzip -d /android /tmp/sdk-tools-linux-4333796.zip ;

ENV ANDROID_HOME=/android
ENV PATH=${ANDROID_HOME}:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/tools:${PATH}

# install android
RUN yes | sdkmanager --licenses ; \
    yes | android update sdk --no-ui --all --filter android-26 ; \
    yes | android update sdk --no-ui --all --filter tool ; \
    yes | android update sdk --no-ui --all --filter extra-android-m2repository ; \
    yes | android update sdk --no-ui --all --filter build-tools-27.0.3 ;

# install dependencies
RUN pip3 install pillow ; \
    pip3 install ConfigParser ; \
    pip3 install pycrypto ; \
    pip3 install requests ; \
    npm install -g cordova@8.1.2 ; \
    npm install -g bower ; \
    npm install -g grunt@0.4.5 ; \
    npm install -g grunt-cli@1.2.0 ; \
    npm install -g gulp ; \
    npm install -g gulp-cli ;

# imagemagic
RUN apt-get update ; \
    apt-get install -y imagemagick ;

# install appcenter cli
RUN npm install -g appcenter-cli ;

# install jq
RUN apt-get install -y jq ;

ADD VERSION .