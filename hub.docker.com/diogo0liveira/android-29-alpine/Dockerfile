FROM adoptopenjdk/openjdk8:alpine
LABEL maintainer="Diogo Oliveira <diogo0liveira@hotmail.com>"

RUN apk add --no-cache \
	wget \
	unzip && \
	apk add --virtual .rundeps $runDeps && \
	rm -rf /tmp/* && \
	rm -rf /var/cache/apk/*

ENV ANDROID_HOME "/opt/sdk"
ENV PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools

COPY debug.keystore /

RUN mkdir -p ~/.android/ && touch ~/.android/repositories.cfg && mv debug.keystore ~/.android/
RUN mkdir -p ${ANDROID_HOME}

RUN wget -q https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -O /tmp/tools.zip && \
	unzip -qq /tmp/tools.zip -d ${ANDROID_HOME} && \
	rm -v /tmp/tools.zip

RUN yes | \
	${ANDROID_HOME}/tools/bin/sdkmanager "--licenses" && \
	${ANDROID_HOME}/tools/bin/sdkmanager --verbose "platform-tools" && \
	${ANDROID_HOME}/tools/bin/sdkmanager --verbose "extras;android;m2repository" && \
	${ANDROID_HOME}/tools/bin/sdkmanager --verbose "extras;google;m2repository" && \
	${ANDROID_HOME}/tools/bin/sdkmanager --verbose "extras;google;instantapps" && \
	${ANDROID_HOME}/tools/bin/sdkmanager --verbose "platforms;android-29" && \
	${ANDROID_HOME}/tools/bin/sdkmanager --verbose "build-tools;29.0.2" && \
	${ANDROID_HOME}/tools/bin/sdkmanager --verbose "--update"
