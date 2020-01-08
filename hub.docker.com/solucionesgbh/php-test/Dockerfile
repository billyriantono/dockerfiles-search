FROM php:7.1.1

# Install dependencies
RUN apt-get update -yqq && apt-get install -yqq curl zip git libcurl4-gnutls-dev \
	libicu-dev libmcrypt-dev libvpx-dev libjpeg-dev libpng-dev libxpm-dev zlib1g-dev \
	libfreetype6-dev libxml2-dev libexpat1-dev libbz2-dev libgmp3-dev libldap2-dev \
	unixodbc-dev libpq-dev libsqlite3-dev libaspell-dev libsnmp-dev libpcre3-dev \
	libtidy-dev

# Install PECL extensions
RUN pecl install xdebug-2.5.0 \
    && docker-php-ext-enable xdebug

# Install php extentions
RUN docker-php-ext-install mbstring mcrypt pdo_mysql pdo_pgsql curl json intl gd xml zip bz2 opcache

# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php && \
	php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
	php -r "unlink('composer-setup.php');"

CMD ["php", "-a"]