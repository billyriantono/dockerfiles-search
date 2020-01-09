FROM halito/php-apache:7.2.5
MAINTAINER halito! <devs@halito.com>

# Install Composer
RUN curl -s http://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Install Xdebug
RUN pecl install xdebug-2.6.0 \
    && docker-php-ext-enable xdebug

# Read files using nano
RUN apt-get update
RUN apt-get install unzip

# Install PHPUnit-
RUN composer global require phpunit/phpunit