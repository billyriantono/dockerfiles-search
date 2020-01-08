FROM java:8-jdk

MAINTAINER itog <itog@pigmal.com>

ENV DEBIAN_FRONTEND noninteractive

RUN dpkg --add-architecture i386
RUN apt-get update -y && apt-get upgrade -y
RUN echo y | apt-get install libncurses5:i386 libstdc++6:i386 zlib1g:i386

# Install Gradle.
RUN echo "deb http://ppa.launchpad.net/cwchien/gradle/ubuntu trusty main" | tee /etc/apt/sources.list.d/cwchien-gradle.list && \
	echo "deb-src http://ppa.launchpad.net/cwchien/gradle/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/cwchien-gradle.list && \
	apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
	apt-get update -y && \
	apt-get install  -y --force-yes --no-install-recommends gradle-2.14 && \
	apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
ENV GRADLE_HOME=/usr/lib/gradle/2.14/ \
	TERM=dumb


# Install Android SDK.
ENV ANDROID_SDK_URL=http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz \
	ANDROID_HOME=/opt/android-sdk-linux \
	ANDROID_SDK=/opt/android-sdk-linux
RUN apt-get update -y && \
	apt-get install -y --force-yes --no-install-recommends curl expect && \
	curl -L ${ANDROID_SDK_URL} | tar --no-same-owner -xz -C /opt && \
	apt-get autoremove -y --purge curl && \
	apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
ENV PATH $ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$PATH


# Install Android packages.
RUN echo y | android update sdk --no-ui --force --all --filter "tools"
RUN echo y | android update sdk --no-ui --force --all --filter "platform-tools"
RUN echo y | android update sdk --no-ui --force --all --filter "build-tools-23.0.3,build-tools-23.0.2,build-tools-23.0.1"
RUN echo y | android update sdk --no-ui --force --all --filter "android-23,android-22,android-21"
RUN echo y | android update sdk --no-ui --force --all --filter "extra-android-m2repository,extra-google-google_play_services,extra-google-m2repository"

ENV DEBIAN_FRONTEND dialog
