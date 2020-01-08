#!/bin/bash

FROM dockette/stretch

RUN \
	mkdir /run/php


RUN \
	apt-get update -y && \
	apt-get dist-upgrade -y && \
	apt-get update -y && \
	apt-get install -y wget curl apt-transport-https ca-certificates git lsb-release supervisor vim mc htop poppler-utils gnupg && \
	wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
	echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list && \
	export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
	echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
	curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
	apt-get update -y && \
	apt-get install -y php7.2-fpm nginx php7.2-xml php7.2-zip php7.2-mysqli mariadb-client php7.2-mbstring php7.2-gd google-cloud-sdk zip

CMD ["/bin/bash"]
