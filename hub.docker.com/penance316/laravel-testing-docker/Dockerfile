FROM php:7-fpm
RUN pecl channel-update pecl.php.net
RUN apt-get update && apt-get install -qy git curl libmcrypt-dev mysql-client zip unzip
RUN pecl install mcrypt-1.0.2