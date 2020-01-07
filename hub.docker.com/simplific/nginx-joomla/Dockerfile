FROM simplific/nginx-php

ENV JOOMLA_VERSION 3.4.8

ADD files/01-joomla.conf /etc/nginx/conf.d/01-joomla.conf

RUN 	apk --no-cache --update add curl unzip php-dom \
	&& curl -L "https://github.com/joomla/joomla-cms/releases/download/${JOOMLA_VERSION}/Joomla_${JOOMLA_VERSION}-Stable-Full_Package.zip" -o "joomla.zip" \
	&& mkdir -p /opt/joomla \
	&& unzip joomla.zip -d /opt/joomla \
	&& rm joomla.zip \
	&& chown -R nginx:www-data /opt/joomla

VOLUME "/opt/joomla/"
