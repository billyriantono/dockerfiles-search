FROM php:7.2-fpm
LABEL maintainer="Benjamin Lu ( ben@getbenonit.com )"

# install the PHP extenstion we need ( https://make.wordpress.org/hosting/handbook/handbook/server-environment/#php-extensions )
RUN set -ex; \
    savedAptMark="$(apt-mark showmanual)"; \
    apt-get update; \
    apt-get install --no-install-recommends -y \
		libjpeg-dev \
		libmagickwand-dev \
		libpng-dev \
		libzip-dev \
    ; \
    docker-php-ext-install \
        bcmath \
        exif \
        gd \
        mysqli \
        opcache \
        zip \
    ; \
    pecl install imagick-3.4.4; \
    docker-php-ext-enable imagick; \
    # reset apt-mark's "manual" list so that "purge --auto-remove" will remove all build dependencies
	apt-mark auto '.*' > /dev/null; \
	apt-mark manual $savedAptMark; \
	ldd "$(php -r 'echo ini_get("extension_dir");')"/*.so \
		| awk '/=>/ { print $3 }' \
		| sort -u \
		| xargs -r dpkg-query -S \
		| cut -d: -f1 \
		| sort -u \
		| xargs -rt apt-mark manual; \
	\
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
    rm -rf /var/lib/apt/lists/*

COPY php-fpm/7.2/mailhog/mhsendmail /usr/local/bin/mhsendmail
RUN echo 'sendmail_path = /usr/local/bin/mhsendmail --smtp-addr mailhog:1025' > /usr/local/etc/php/conf.d/mailhog.ini

RUN curl --silent -L -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x /usr/local/bin/wp

RUN usermod -u 1000 www-data