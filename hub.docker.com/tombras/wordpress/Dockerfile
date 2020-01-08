FROM wordpress:php7.2

# Setup sendmail for local email testing
RUN apt-get update && apt-get install -y -qq \
	sendmail \
	sendmail-bin \
	mailutils \
	libmagickwand-dev \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libpng-dev \
	libjpeg-dev \
	libpq-dev \
	libmcrypt-dev \
	libldap2-dev \
	libldb-dev \
	libicu-dev \
	libgmp-dev \
	libxml2-dev \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install gd soap\
	mysqli \
	opcache \
	pdo \
	pdo_mysql \
	pdo_pgsql \
	pgsql \
	ldap \
	intl \
	gmp \
	zip \
	bcmath \
	mbstring \
	pcntl \
	&& rm -rf /var/lib/apt/lists/*



# Config sendmail
RUN { \
	echo "sendmail_path = /usr/sbin/sendmail -t -i"; \
	echo "SMTP = localhost"; \
	echo "smtp_port = 25"; \
	} >  /usr/local/etc/php/conf.d/dockerfile-mail.ini

RUN { \
	echo "short_open_tag=Off"; \
	} >  /usr/local/etc/php/conf.d/dockerfile-php.ini

# Setup XDebug
RUN yes | pecl install xdebug-beta \
	&& echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/dockerfile-xdebug.ini \
	&& echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/dockerfile-xdebug.ini \
	&& echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/dockerfile-xdebug.ini \
	&& echo "xdebug.profiler_output_dir=/home/LogFiles" >> /usr/local/etc/php/conf.d/dockerfile-xdebug.ini \
	&& echo "xdebug.remote_host=host.docker.internal" >> /usr/local/etc/php/conf.d/dockerfile-xdebug.ini

# Setup additional PHP extensions
RUN pecl install redis imagick-beta mcrypt-1.0.1

RUN docker-php-ext-enable redis imagick mcrypt

# Setup self-signed ssl
RUN openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout /etc/ssl/private/ssl-cert-snakeoil.key -out /etc/ssl/certs/ssl-cert-snakeoil.pem -subj "/C=US/ST=Tennessee/L=Knoxville/O=Agency/OU=Development/CN=*.tombrasweb.com"

# Setup apache modules
RUN a2enmod rewrite ssl headers && a2ensite default-ssl

# Setup Wordpress starter files
RUN mkdir /usr/src/starter-files
COPY starter-files/* /usr/src/starter-files/

EXPOSE 80
EXPOSE 443

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]
