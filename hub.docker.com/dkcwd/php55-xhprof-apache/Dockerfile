FROM php:5.5.37-apache
RUN pecl install -f xhprof && docker-php-ext-enable xhprof
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y graphviz
