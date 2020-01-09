FROM php:7.2-apache

RUN apt-get update && apt-get -y install curl wget && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo pdo_mysql

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
EXPOSE 80
EXPOSE 443

ENV VERSION 3.1.1
ENV PHPMONITOR_URL https://sourceforge.net/projects/phpservermon/files/phpservermon/PHP%20Server%20Monitor%20v$VERSION/phpservermon-$VERSION.tar.gz

RUN set -x \
	&& rm -rf /var/www/html/* \
	&& wget $PHPMONITOR_URL -P /tmp\
	&& tar -xvf /tmp/phpservermon-$VERSION.tar.gz -C /tmp --strip-components=1 \
	&& mv /tmp/phpservermon-$VERSION/* /var/www/html \
	&& touch /var/www/html/config.php \
	&& chmod 0777 /var/www/html/config.php
