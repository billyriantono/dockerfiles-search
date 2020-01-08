FROM php:5.6.32-apache
 
RUN apt-get update \
 && apt-get install -y --no-install-recommends $PHPIZE_DEPS libicu52 libicu-dev libmcrypt4 libmcrypt-dev libmemcached11 libmemcached-dev libpq5 libpq-dev libsasl2-dev zlib1g zlib1g-dev \
 && pecl install memcached-2.1.0 redis \
 && docker-php-ext-enable memcached redis \
 && docker-php-ext-install bcmath intl mbstring mcrypt opcache pdo_mysql pdo_pgsql zip \
 && apt-get -y remove libicu-dev libmcrypt-dev libmemcached-dev libpq-dev libsasl2-dev zlib1g-dev \
 && rm -r /var/lib/apt/lists/*

RUN apt-get update \
 && apt-get install -y --no-install-recommends git make openssh-client \
 && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php composer-setup.php --filename=composer --install-dir=/usr/local/bin \
 && php -r "unlink('composer-setup.php');" \
 && rm -r /var/lib/apt/lists/*

COPY 000-default.conf /etc/apache2/sites-available/
