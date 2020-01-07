FROM tcloud/ubuntu-jdk:8
MAINTAINER tcloud

USER root

ENV DEBIAN_FRONTEND="noninteractive" \
	LC_ALL="en_US.UTF-8" \
    ANDROID_BUILD_TOOLS_VERSION="23.0.3" \
    ANDROID_SDK_VERSION="r24.4.1" \
    ANDROID_NDK_VERSION="r11c" \
    ANT_VERSION="1.9.7" \
    MAVEN_VERSION="3.3.9" \
    GRADLE_VERSION="2.12"

# Fake a fuse install (to prevent ia32-libs-multiarch package from producing errors)
RUN cd /tmp && \
	apt-get update && \ 
	apt-get install -y libfuse2 && \
	apt-get download fuse && \
	dpkg-deb -x fuse_* . && \
	dpkg-deb -e fuse_* && \
	rm fuse_*.deb && \
	echo -en '#!/bin/bash\nexit 0\n' > DEBIAN/postinst && \
	dpkg-deb -b . /fuse.deb && \
	dpkg -i /fuse.deb

# Install Deps
RUN dpkg --add-architecture i386 && \
	apt-get install -y --force-yes \
		git \
		wget \
		python \
		python-software-properties \
		curl \
		expect \
		bzip2 \
		libc6-i386 \
		lib32stdc++6 \
		lib32ncurses5 \
		lib32z1 \
		lib32gcc1 \
		lib32ncurses5 \
		lib32bz2-1.0 \
		g++-multilib \
		net-tools \
		p7zip-full

# Install Android SDK
RUN cd /opt/ && \
	curl -sLO http://dl.google.com/android/android-sdk_${ANDROID_SDK_VERSION}-linux.tgz && \ 
	tar xzf android-sdk_${ANDROID_SDK_VERSION}-linux.tgz && \ 
	chown -R root:root /opt/android-sdk-linux && \
	ln -s android-sdk-linux android-sdk && \
	rm -f android-sdk_${ANDROID_SDK_VERSION}-linux.tgz

# Install android ndk
RUN cd /opt/ && \
	curl -sLO http://dl.google.com/android/repository/android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip && \
	7z x android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip && \
	ls -lh && \
	ln -s android-ndk-${ANDROID_NDK_VERSION} android-ndk && \
	rm -rf android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip

# Install android ndk r10e
# RUN cd /opt/ && \
# 	curl -sLO http://dl.google.com/android/ndk/android-ndk-r10e-linux-x86_64.bin && \
# 	chmod a+x ./android-ndk-r10e-linux-x86_64.bin && \
# 	./android-ndk-r10e-linux-x86_64.bin && \
# 	ls -lh && \
# 	ln -s android-ndk-r10e android-ndk && \
# 	rm -rf android-ndk-r10e-linux-x86_64.bin

# Install apache ant
RUN cd /opt/ && \
	curl -sLO http://archive.apache.org/dist/ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
	tar -xzf apache-ant-${ANT_VERSION}-bin.tar.gz && \
	ls -lh && \
	ln -s apache-ant-${ANT_VERSION} ant && \
	rm -rf apache-ant-${ANT_VERSION}-bin.tar.gz

# # Install Maven 3
RUN cd /opt/ && \
	curl -sLO http://apache.mirror.anlx.net/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    tar -xzf apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    ls -lh && \
    ln -s apache-maven-${MAVEN_VERSION} maven  && \
    rm -f apache-maven-${MAVEN_VERSION}-bin.tar.gz

# Install Gradle
RUN cd /opt/ && \
	curl -sLO https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-all.zip && \
	7z x gradle-${GRADLE_VERSION}-all.zip && \
	ls -lh && \
	ln -s gradle-${GRADLE_VERSION} gradle && \
	rm -rf gradle-${GRADLE_VERSION}-all.zip

# Add android tools and platform tools to PATH
ENV ANDROID_HOME="/opt/android-sdk" \
	ANDROID_SDK_HOME="/opt/android-sdk" \
	ANDROID_NDK_HOME="/opt/android-ndk" \
	ANT_HOME="/opt/ant" \
    MAVEN_HOME="/opt/maven" \
    GRADLE_HOME="/opt/gradle"

ENV PATH ${PATH}:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION:$ANT_HOME/bin:$MAVEN_HOME/bin:$GRADLE_HOME/bin

RUN echo ANDROID_HOME="$ANDROID_HOME" >> /etc/environment && \
	echo ANDROID_SDK_HOME="$ANDROID_SDK_HOME" >> /etc/environment && \
	echo ANDROID_NDK_HOME="$ANDROID_NDK_HOME" >> /etc/environment && \
	echo ANT_HOME="$ANT_HOME" >> /etc/environment && \
	echo MAVEN_HOME="$MAVEN_HOME" >> /etc/environment && \
	echo GRADLE_HOME="$GRADLE_HOME" >> /etc/environment && \
	mkdir -p /data && \
	rm -rf /etc/service/sshd /etc/service/syslog-forwarder /etc/service/syslog-ng

WORKDIR /data

VOLUME ["/root/.gradle/caches", "/data","/log"]

CMD ["/sbin/my_init"]

RUN echo y | /opt/android-sdk/tools/android update sdk --no-ui --all --filter platform-tools,tools,build-tools-20.0.0,build-tools-21.0.0,build-tools-21.1.0,build-tools-21.1.2,build-tools-22.0.1,build-tools-23.0.2,build-tools-23.0.3,android-23,android-21,android-19,addon-google_apis_x86-google-21,extra-android-support,extra-android-m2repository,extra-google-m2repository,extra-google-google_play_services && \
	mkdir -p /opt/android-sdk/tools/keymaps && \
	touch /opt/android-sdk/tools/keymaps/en-us

# RUN echo y | /opt/android-sdk/tools/android update sdk --no-ui --all --filter \
# 	platform-tools, \
# 	tools, \
# 	build-tools-20.0.0, \
# 	build-tools-21.0.0, \
# 	build-tools-21.1.0, \
# 	build-tools-21.1.2, \
# 	build-tools-22.0.1, \
# 	build-tools-23.0.2, \
# 	build-tools-23.0.3, \
# 	android-23, \
# 	android-21, \
# 	android-19, \
# 	addon-google_apis_x86-google-21, \
# 	extra-android-support, \
# 	extra-android-m2repository, \
# 	extra-google-m2repository, \
# 	extra-google-google_play_services && \
# 	mkdir -p /opt/android-sdk/tools/keymaps && \
# 	touch /opt/android-sdk/tools/keymaps/en-us

# Clean up
RUN apt-get clean && \
	apt-get autoremove -y && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*