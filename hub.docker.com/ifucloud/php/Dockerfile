FROM php:5.6-fpm

ENV DRUSH_VERSION 8.1.2
ENV APP_ROOT /var/www/html

RUN apt-get clean -y

# Install the PHP extensions we need
RUN apt-get update && \
apt-get install -y --no-install-recommends \
    curl \
    git \
    mysql-client \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libicu-dev \
    libssl-dev \
    zlib1g-dev \
    libmcrypt-dev && \
    docker-php-ext-configure gd \
        --enable-gd-native-ttf \
        --with-freetype-dir=/usr/include/freetype2 \
        --with-png-dir=/usr/include \
        --with-jpeg-dir=/usr/include && \
    docker-php-ext-install gd pdo_mysql mysqli mysql opcache intl bcmath zip && \
    docker-php-ext-enable bcmath zip pdo_mysql mysqli mysql

# Install Redis
RUN pecl install redis -y && docker-php-ext-enable redis

# Install drush command
RUN curl -fsSL -o /usr/local/bin/drush "https://github.com/drush-ops/drush/releases/download/$DRUSH_VERSION/drush.phar" && \
    chmod +x /usr/local/bin/drush

# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php \
		&& php composer-setup.php \
		&& php -r "unlink('composer-setup.php');" \
		&& mv composer.phar /usr/local/bin/composer

# add timezone
RUN echo 'date.timezone = Asia/Shanghai' >> /usr/local/etc/php/conf.d/docker-php-data-time.ini

VOLUME $APP_ROOT
WORKDIR $APP_ROOT
