FROM php:5.6-apache

# Dependencies
RUN apt-get update \
    && apt-get install -y \
        bash \
        autoconf \
        git \
        libpcre3 libpcre3-dev \
        gcc \
        g++ \
        make \
        openssh-client \
        libcurl4-gnutls-dev \
        zlib1g \
        libfreetype6-dev  \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libmcrypt-dev \
        libssl-dev \
        libxml2-dev \
        libyaml-dev \
        libmemcached-dev \
        libsqlite3-dev \
    && rm -rf /var/cache/apt/archives/*

# Core ext
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install \
        curl \
        zip \
        gd \
        mbstring \
        mcrypt \
        mysqli \
        mysql \
        pdo_mysql \
        soap \
        pcntl \
        pdo_sqlite \
	calendar \
    && rm -rf /usr/src/php/ext/*

# Pecl ext
RUN pecl install \
    redis \
    yaml-1.3.0 \
    apcu-4.0.10 \
    mongodb \
    && docker-php-ext-enable \
        redis \
        yaml \
        apcu \
        mongodb \
    && rm -rf /usr/src/php/ext/*

# Extra ext
RUN git clone https://github.com/php-memcached-dev/php-memcached.git /usr/src/php/ext/memcached/ \
    && cd /usr/src/php/ext/memcached/ && git checkout tags/2.2.0 \
    && docker-php-ext-install memcached \
    && rm -rf /usr/src/php/ext/*

RUN git clone --depth=1 https://github.com/phalcon/cphalcon.git /usr/src/php/ext/phalcon \
    && cd /usr/src/php/ext/phalcon/build && ./install \
    && echo 'extension=phalcon.so' > $PHP_INI_DIR/conf.d/phalcon.ini \
    && rm -rf /usr/src/php/ext/*

# Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && ln -s /usr/bin/composer /usr/local/bin/composer.phar

# PHPUnit
RUN curl -L --silent  https://phar.phpunit.de/phpunit.phar > /usr/local/bin/phpunit \
    && chmod +x /usr/local/bin/phpunit \
    && ln -s /usr/local/bin/phpunit /usr/local/bin/phpunit.phar

# Config
RUN echo "date.timezone=America/Sao_Paulo" > $PHP_INI_DIR/conf.d/date_timezone.ini

# SSH
RUN mkdir /root/.ssh
RUN touch /root/.ssh/known_hosts
RUN ssh-keyscan -t rsa github.com >> /root/.ssh/known_hosts
RUN ssh-keyscan -t rsa bitbucket.org >> /root/.ssh/known_hosts

# Apache mods
RUN a2enmod rewrite

# Image
WORKDIR /var/www/html
