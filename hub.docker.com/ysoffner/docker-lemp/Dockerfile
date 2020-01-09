FROM php:fpm

LABEL maintainer "Yuri Soffner <ysoffner@gmail.com>" \
	Description="Php-fpm Minimizado e atualizado para suportar laravel"

RUN apt-get update -y && apt-get upgrade -y \
  && apt-get install -y vim libcurl4-gnutls-dev libmcrypt-dev  libicu-dev zlib1g-dev zip unzip rsyslog \
  && docker-php-ext-install pdo_mysql iconv intl opcache mbstring curl zip \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
  && curl https://phar.phpunit.de/phpunit.phar -L > phpunit.phar && chmod +x phpunit.phar \
  && mv phpunit.phar /usr/local/bin/phpunit \
  && phpunit --version \
  && rm /etc/localtime \
  && ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime \
  && date \
  && apt-get clean

WORKDIR /var/www