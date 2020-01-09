# From official php-fpm
FROM php:5.6-fpm
LABEL maintainer="Kawin Viriyaprasopsook <bouroo@gmail.com>"

ARG	timezone=Asia/Bangkok
ENV	TERM xterm
ENV	DEBIAN_FRONTEND noninteractive

ENV	LANG en_US.UTF-8
ENV	LC_ALL en_US.UTF-8
ENV	TZ $timezone

# Update OS
RUN	apt-get update && apt-get -y dist-upgrade

# Change locale
RUN	apt-get update && apt-get -y install locales tzdata \
	&& sed -i "s/# th_TH.UTF-8/th_TH.UTF-8/" /etc/locale.gen \
	&& sed -i "s/# en_US.UTF-8/en_US.UTF-8/" /etc/locale.gen \
	&& locale-gen \
	&& update-locale en_US.UTF-8 \
	&& echo $timezone > /etc/timezone \
	&& cp /usr/share/zoneinfo/$timezone /etc/localtime \
	&& dpkg-reconfigure tzdata

# Copy php.ini
# modify from https://github.com/php/php-src/blob/master/php.ini-production
COPY	config/php.ini /usr/local/etc/php/
RUN	chmod 0644 /usr/local/etc/php/php.ini \
	&& sed -i 's/access.log/;access.log/g' /usr/local/etc/php-fpm.d/docker.conf

# Add deps
RUN	apt-get update && apt-get install -y \
	default-libmysqlclient-dev \
	git-core \
	libbz2-dev \
	libc-client-dev \
	libfreetype6-dev \
	libgmp-dev \
	libjpeg-dev \
	libkrb5-dev \
	libmagickwand-dev \
	libmcrypt-dev \
	libmemcached-dev \
	libpng-dev \
	libpq-dev \
	libssh2-1-dev \
	libssl-dev \
	libxml2-dev \
	libzip-dev \
	wget \
	zlib1g-dev \
	nano

# Add PHP ext
RUN	docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
	&& docker-php-ext-install -j$(nproc) \
	bcmath \
	gd \
	#gmp \
	iconv \
	imap \
	json \
	mbstring \
	mysqli \
	pcntl \
	pdo_mysql \
	pdo_pgsql  \
	soap \
	sockets \
	xmlrpc \
	zip
RUN	pecl install memcached-2.2.0 \
	&& pecl install redis-2.2.8 \
	&& pecl install apcu-4.0.11 \
	&& pecl install ssh2-0.13 \
	&& pecl install imagick \
	&& pecl install mongodb
RUN	docker-php-ext-enable memcached redis apcu ssh2 imagick mongodb

# Composer
RUN	php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php \
	&& php composer-setup.php \
	&& php -r "unlink('composer-setup.php');" \
	&& chmod +x composer.phar \
	&& mv composer.phar /usr/bin/composer

# ionCube
RUN	wget -c https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz -O ioncube_loaders_lin_x86-64.tar.gz \
	&& tar -xvzf ioncube_loaders_lin_x86-64.tar.gz \
	&& cp ioncube/ioncube_loader_lin_5.6.so $(php -r 'echo ini_get("extension_dir");')/ \
	&& (echo "zend_extension=ioncube_loader_lin_5.6.so" | tee /usr/local/etc/php/conf.d/00-ioncube-loader.ini || true) \
	&& rm -rf ioncube_loaders_lin_x86-64.tar.gz \
	&& rm -rf ioncube

# Add global composer bin dir to PATH
ENV	PATH /root/.composer/vendor/bin:$PATH

EXPOSE	9000

CMD	["php-fpm", "-F"]
