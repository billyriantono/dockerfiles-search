
ARG OPENJDK=8-jdk
FROM openjdk:${OPENJDK}

MAINTAINER gaoxinio

ARG ANDROID_SDK_VERSION=25.2.4
ARG GRADLE_VERSION=4.3.1

ENV ANDROID_HOME "/opt/sdk"
ENV GRADLE_HOME "/opt/gradle"

ENV PATH=${PATH}:${ANDROID_HOME}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

RUN mkdir -p ${ANDROID_HOME}

ADD sdkupdate ${ANDROID_HOME}
ADD https://dl.google.com/android/repository/tools_r${ANDROID_SDK_VERSION}-linux.zip android-sdk-tools.zip

RUN echo "Installing Android SDK" \
	&& mkdir -p /root/.android/ \
	&& touch /root/.android/repositories.cfg \
 	&& unzip -q /android-sdk-tools.zip -d ${ANDROID_HOME}/  \
 	&& rm -f android-sdk-tools.zip \
 	&& chmod +x ${ANDROID_HOME}/sdkupdate \
    && sync \
    && sdkupdate 

ADD "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" gradle.zip

RUN echo "Installing gradle" \
	&& unzip -q gradle.zip \
	&& mv "gradle-${GRADLE_VERSION}" "${GRADLE_HOME}" \
	&& ls -l ${GRADLE_HOME}/ \
	&& rm -f gradle-${GRADLE_VERSION}.zip \
	&& ln --symbolic "${GRADLE_HOME}/bin/gradle" /usr/bin/gradle \
	&& echo "Test gradle" \
	&& gradle --version