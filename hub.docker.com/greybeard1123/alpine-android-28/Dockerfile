FROM openjdk:8-alpine
LABEL maintainer="Faraz M R. <farazmr@gmail.com>"

ENV SDK_TOOLS "4333796"
ENV BUILD_TOOLS "28.0.3"
ENV TARGET_SDK "28"
ENV ANDROID_HOME "/opt/android/sdk"
ENV PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools

# Install required dependencies
RUN apk add --no-cache wget unzip curl git openssl openssh-client ca-certificates bash

# Download and extract Android Tools
RUN wget http://dl.google.com/android/repository/sdk-tools-linux-${SDK_TOOLS}.zip -O /tmp/tools.zip && \
	mkdir -p ${ANDROID_HOME} && \
	unzip /tmp/tools.zip -d ${ANDROID_HOME} && \
	rm -v /tmp/tools.zip

# Install SDK Packages
RUN mkdir -p /root/.android/ && \
	touch /root/.android/repositories.cfg

RUN yes | sdkmanager --licenses && sdkmanager --update

RUN yes | sdkmanager \
  "tools" \
  "platform-tools" \
  "build-tools;28.0.3" \
  "extras;android;m2repository" \
  "platforms;android-28" \
  "extras;google;m2repository"

