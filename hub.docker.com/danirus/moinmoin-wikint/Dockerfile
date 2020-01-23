FROM php:7
RUN apt-get update && apt-get install -y zlib1g-dev
RUN pecl install grpc && docker-php-ext-enable grpc
