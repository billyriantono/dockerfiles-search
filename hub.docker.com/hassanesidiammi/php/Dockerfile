FROM php:5.6-apache

RUN apt-get update \
	&& apt-get install -y --fix-missing mysql-client \
	&& a2enmod rewrite \
	&& /etc/init.d/apache2 restart \
	&& docker-php-ext-install mbstring pdo pdo_mysql \
  && apt-get install -y vim nano

# Set timezone
RUN rm /etc/localtime \
  && ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime \
  && "date"

# install xdebug
RUN pecl install xdebug \
  && docker-php-ext-enable xdebug \
  && { \
      echo "error_reporting = E_ALL"; \
      echo "display_startup_errors = On"; \
      echo "display_errors = On"; \
      echo "xdebug.remote_enable=1"; \
      echo "xdebug.remote_connect_back=1"; \
      echo "xdebug.idekey=\"PHPSTORM\""; \
      echo "xdebug.remote_port=9001"; \
    } >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

EXPOSE 9001


RUN {\
      echo 'alias sf="php bin/console"'; \
      echo 'export TERM=xterm'; \
    } >> ~/.bashrc \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /var/www/symfony \
  && mkdir -p /usr/local/bin \
  && curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony \
  && chmod a+x /usr/local/bin/symfony \
  && echo "Type \"symfony new symfony\" to create a new Project"

WORKDIR /var/www/symfony

