FROM php:7-fpm

RUN apt-get -y update \
  && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    php5-json \
    php5-mysql \
    git zip unzip \
  && docker-php-ext-install -j$(nproc) iconv mcrypt pdo pdo_mysql\
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && curl -sS https://getcomposer.org/installer \
    | php -- --install-dir=/usr/local/bin --filename=composer

# ADD ./polr /var/www/polr
RUN git clone https://github.com/cydrobolt/polr.git /var/www/polr
RUN chown -R www-data:www-data /var/www/
WORKDIR /var/www/polr

RUN composer install --no-dev -o
