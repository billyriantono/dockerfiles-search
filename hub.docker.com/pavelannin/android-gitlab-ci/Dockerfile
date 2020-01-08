FROM openjdk:8-jdk
MAINTAINER Pavel Annin

ENV VERSION_SDK_TOOLS "4333796"
ENV ANDROID_HOME "/opt/android-sdk"

ENV ANDROID_BUILD_TOOLS "28.0.3"
ENV ANDROID_TARGET_SDK "28"

# Install required dependency 
RUN dpkg --add-architecture i386
RUN apt-get -qq update
RUN apt-get install -y --no-install-recommends \
	libc6:i386 \
	libstdc++6:i386 \
	libgcc1:i386 \
	libncurses5:i386 \
	libz1:i386 \
	wget \
	curl \
	unzip \
	locales \
	git-core \
	file \	
	ruby \
    ruby-dev \
    build-essential
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - 
RUN apt-get install -y --no-install-recommends nodejs
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Fastlane
RUN gem install fastlane -NV

# Install App center
RUN npm install -g appcenter-cli

# Install android SDK tools
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-${VERSION_SDK_TOOLS}.zip -O /tmp/tools.zip && \
	mkdir -p ${ANDROID_HOME} && \
	unzip /tmp/tools.zip -d ${ANDROID_HOME} && \
	rm -v /tmp/tools.zip
RUN mkdir -p /root/.android/ && touch /root/.android/repositories.cfg && \
	yes | ${ANDROID_HOME}/tools/bin/sdkmanager "--licenses" && \
	${ANDROID_HOME}/tools/bin/sdkmanager "--update" && \
	${ANDROID_HOME}/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS}" "platform-tools" "platforms;android-${ANDROID_TARGET_SDK}" "extras;android;m2repository" "extras;google;google_play_services" "extras;google;m2repository" "emulator"
