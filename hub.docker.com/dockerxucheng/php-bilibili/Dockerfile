FROM php:7.2-fpm
RUN apt-get update \
    && apt-get -y install iputils-ping \
    && apt-get -y install zlib1g-dev \
	&& pecl install redis-4.0.1 \
    && pecl install xdebug-2.6.0 \
    && pecl install yaf \
    && pecl install grpc \
    && pecl install protobuf \
    && docker-php-ext-install mysqli \
    && docker-php-ext-enable redis xdebug yaf grpc protobuf mysqli