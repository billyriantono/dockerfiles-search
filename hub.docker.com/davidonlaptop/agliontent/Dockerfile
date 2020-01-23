FROM php:7.3-apache

# Install PHP extensions
RUN apt-get update && apt-get install -y \
      libicu-dev \
      libpq-dev \
      libmcrypt-dev \
      zlib1g-dev \
      libcurl4-gnutls-dev \
      libfreetype6-dev \
      libjpeg62-turbo-dev \
      libzip-dev \
      libpng-dev \
      mariadb-client \
      unzip \
      git \
      rsync \
      wget \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-install \
      exif \
      intl \
      mbstring \
      pcntl \
      mysqli \
      pdo \
      pdo_mysql \
      zip \
      opcache \
      curl \
      gd

# Store PHP Configs at /usr/local/etc/php/conf.d
RUN echo "upload_max_filesize = 1G" >> /usr/local/etc/php/conf.d/upload_large_dumps.ini \
    && echo "post_max_size = 1G" >> /usr/local/etc/php/conf.d/upload_large_dumps.ini

# Change uid and gid of apache to docker user uid/gid
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN composer config --global repo.packagist composer https://packagist.org