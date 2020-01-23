FROM php:7-fpm

RUN apt-get update \
  && apt-get install -y --no-install-recommends ssmtp libpq-dev libmagickwand-dev \
  && docker-php-ext-install mysqli pdo_pgsql pdo_mysql
RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev libpq-dev \
&& rm -rf /var/lib/apt/lists/* \
&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
&& docker-php-ext-install gd mbstring pdo pdo_mysql pdo_pgsql \
&& pecl install imagick  \
&& docker-php-ext-enable imagick
