FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive

RUN set -ex; apt-get update \
	&& apt-get -y install openjdk-8-jdk git php7.0-cgi php7.0 php7.0-xml php7.0-mbstring php7.0-zip composer curl gnupg \
	&& curl -sL https://deb.nodesource.com/setup_8.x | bash - \
	&& apt-get -y install nodejs \
	&& export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" \
	&& echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list \
	&& curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
	&& apt-get update && apt-get -y install google-cloud-sdk \
	#&& npm install -g firebase-tools \
	&& useradd -m jenkins


CMD [ "bash" ]
