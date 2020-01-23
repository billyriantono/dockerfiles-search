FROM php:7.3
LABEL maintainer="CWallenberg" \
    node="10" \
    php="7.3"

WORKDIR /var/www
#COPY . /var/www

# COPY INSTALL SCRIPTS
COPY ./scripts/*.sh /var/www/
RUN chmod +x /var/www/*.sh

# Env variables
ENV PATH=$HOME/.yarn/bin:$PATH

# Install PHP extensions and PECL modules.
RUN buildDeps=" \
        default-libmysqlclient-dev \
        libbz2-dev \
        libsasl2-dev \
    " \
    runtimeDeps=" \
        apt-utils \
        curl \
        g++ \
        gcc \
        git \
        gnupg2 \
        lftp \
        libfreetype6-dev \
        libicu-dev \
        libjpeg-dev \
        libldap2-dev \
        libpng-dev \
        libpq-dev \
        libxml2-dev \
        libzip-dev \
		libgmp-dev \
        make \
        wget \
    " \
    && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y $buildDeps $runtimeDeps \
    && bash ./nodejs.sh \
    && docker-php-ext-install bcmath bz2 calendar iconv intl mbstring mysqli opcache pdo_mysql soap zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
	&& docker-php-ext-configure gmp \
	&& docker-php-ext-install gmp \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-install ldap \
    && docker-php-ext-install exif \
    && apt-get purge -y --auto-remove $buildDeps \
    && rm -r /var/lib/apt/lists/* \
    # Install Composer.
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && ln -s $(composer config --global home) /root/composer
ENV PATH=$PATH:/root/composer/vendor/bin COMPOSER_ALLOW_SUPERUSER=1

#RUN composer install --no-dev
