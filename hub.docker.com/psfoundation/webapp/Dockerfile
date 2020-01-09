FROM php:5.6.29-apache
MAINTAINER Przemek Szalko <przemek@rentcars.pl>

# 1. Configure runtime environment
# 2. Install nodejs
# 3. Install *-dev packages for PHP modules
# 4. Install PHP modules
# 5. Install PHP Composer
RUN apt-get update \
    && apt-get install -y \
		ntp \
		mysql-client \
	    git \
		zip \
		bzip2 \
		exim4 \
        libbz2-dev \
        libfreetype6-dev \
        libjpeg-dev \
        libmcrypt-dev \
        libpng12-dev \
        libvpx-dev \
		libfontconfig1 \
	&& curl -sL https://deb.nodesource.com/setup_5.x | bash - \	
	&& apt-get install -y nodejs \
	&& rm -rf /var/lib/apt/lists/ \
	&& docker-php-ext-install bz2 \
                        calendar \
                        exif \
                        fileinfo \
                        mbstring \
                        mcrypt \
                        opcache \
						mysqli \
                        pdo_mysql \
    && docker-php-ext-configure gd \
               --with-vpx-dir=/usr/lib/x86_64-linux-gnu \
               --with-jpeg-dir=/usr/lib/x86_64-linux-gnu \
               --with-png-dir=/usr/lib/x86_64-linux-gnu \
               --with-freetype-dir=/usr/lib/x86_64-linux-gnu \
    && docker-php-ext-install gd \
	&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install php-redis
RUN curl -s -L -o /usr/src/phpredis.tar.gz https://github.com/phpredis/phpredis/archive/2.2.7.tar.gz \
	&& mkdir -p /usr/src/phpredis \
	&& tar --strip-components=1 -C /usr/src/phpredis -zxvf /usr/src/phpredis.tar.gz \
	&& cd /usr/src/phpredis \
	&& phpize \
	&& ./configure \
	&& make \
	&& make install \
	&& rm -rf /usr/src/phpredis* \
	&& echo "extension=redis.so" > /usr/local/etc/php/conf.d/php-redis.ini
						
# Configure PHP
COPY conf/php/php.ini ${PHP_INI_DIR}/php.ini

# Entrypoint
COPY entrypoint.sh /entrypoint.sh

# 1. Configure services
# 2. Configure environment + timezone
# 3. Clean up image
COPY conf /tmp/conf
RUN useradd -d /webapps -U -s /bin/bash webapps \
	&& mkdir /webapps \
	&& chown -R webapps.webapps /webapps \
	&& /tmp/conf/configure-apache2.sh \
	&& /tmp/conf/configure-exim4.sh \
	&& chmod 0700 /entrypoint.sh \
	&& ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime \
	&& rm -rf /tmp/conf \
	&& apt-get clean

# Configure runtime environment
EXPOSE 80

ENV TERM="xterm" \
	APPLICATION_ENV="" \
	VIRTUAL_HOST=""

ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2-foreground"]

