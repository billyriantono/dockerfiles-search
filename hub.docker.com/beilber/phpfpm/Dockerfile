FROM php:5.6-fpm
MAINTAINER beilber brian.eilber@gmail.com
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
	nginx \
	git \
    && docker-php-ext-install iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

EXPOSE 9000 
VOLUME ["/var/run/php5-fpm.sock"]
ADD scripts/start /start
CMD ["/start && php-fpm"]
