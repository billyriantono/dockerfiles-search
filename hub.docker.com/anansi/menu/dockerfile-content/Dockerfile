FROM openjdk:8

ENV SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip" \
	ANDROID_HOME="/usr/local/android-sdk" \
	ANDROID_VERSION=28 \
	ANDROID_BUILD_TOOLS_VERSION=27.0.3

RUN mkdir "$ANDROID_HOME" .android \
	&& cd "$ANDROID_HOME" \
	&& curl -o sdk.zip $SDK_URL \
	&& unzip sdk.zip \
	&& rm sdk.zip \
	&& yes | $ANDROID_HOME/tools/bin/sdkmanager --licenses

# Install Android Build Tool and Libraries
RUN $ANDROID_HOME/tools/bin/sdkmanager --update
RUN $ANDROID_HOME/tools/bin/sdkmanager "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" \
	"platforms;android-${ANDROID_VERSION}" \
	"platform-tools"

# Install yarn and node
RUN apt-get update
RUN apt-get install -y apt-transport-https
RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
RUN chmod +x nodesource_setup.sh
RUN ./nodesource_setup.sh
RUN apt-get update
RUN apt-get install -y build-essential \
	nodejs \
	ruby-dev \
	dh-autoreconf 
# Install fast-lane
RUN gem install fastlane -NV
RUN curl -o- -L https://yarnpkg.com/install.sh | bash
RUN mkdir /application
WORKDIR /application

RUN echo '#!/bin/bash\n\
	chmod +x ./android/gradlew\n\
	yarn install --production --network-concurrency 1 || exit 1\n\
	if [ $# -eq 0 ]\n\
	then\n\
	echo ERROR: "set of commands to run are not provided"\n\
	exit 1\n\
	else\n\
	for arg in "$@"\n\
	do\n\
	finalcmd="$finalcmd $arg"\n\
	done\n\
	(cd ./android; $finalcmd)\n\
	fi' >> /android-build

RUN chmod +x /android-build
ENTRYPOINT ["/android-build"]
#CMD []
