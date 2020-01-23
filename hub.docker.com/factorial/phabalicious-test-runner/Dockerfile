FROM php:7.1-cli-alpine
RUN docker-php-ext-install bcmath
RUN apk update && apk upgrade && apk add --no-cache bash git openssh docker
RUN curl --silent --show-error https://getcomposer.org/installer | php
