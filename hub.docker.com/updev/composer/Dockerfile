# Composer Docker Container
FROM composer/composer
MAINTAINER Ladygin Sergey <sladygin@updev.ru>

# ext bcmath pour client RabbitMQ
RUN docker-php-ext-configure bcmath
RUN docker-php-ext-install bcmath