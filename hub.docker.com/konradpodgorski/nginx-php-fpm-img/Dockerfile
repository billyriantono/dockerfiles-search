FROM bpol/nginx-php-fpm

MAINTAINER Konrad Podgórski <konrad.podgorski@gmail.com>

USER root

RUN apt-get update || apt-get update

RUN apt-get install -y jpegoptim optipng pngquant gifsicle redis-server

RUN apt-get install -y \
    libmagickwand-dev --no-install-recommends \
    && pecl install imagick \
	&& docker-php-ext-enable imagick
