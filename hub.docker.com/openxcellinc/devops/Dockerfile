FROM php:7.1-fpm
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN apt-get update && apt-get install -y \
libicu-dev \
libpq-dev \
libmcrypt-dev \
mysql-client \
git \
zip \
libcurl3-dev \
unzip \
libfreetype6-dev \
libjpeg62-turbo-dev \
libmcrypt-dev \
&& rm -r /var/lib/apt/lists/* \
&& docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
&& docker-php-ext-install \
curl \
mbstring \
exif \
hash \
json \
mysqli \
pdo_mysql \
pdo_pgsql \
pgsql \
posix \
session
RUN docker-php-ext-install -j$(nproc) iconv mcrypt 
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd
