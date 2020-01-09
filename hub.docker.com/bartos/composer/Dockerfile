FROM php:7.0-cli
MAINTAINER Vojtech Bartos <docker@vojtechbartos.com>

# Install modules
RUN apt-get update \
    && apt-get install -y git zlib1g-dev \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install zip

ENV COMPOSER_VERSION 1.0.1

VOLUME /project
WORKDIR /project

RUN php -r "readfile('https://getcomposer.org/installer');" > /tmp/composer-setup.php \
    && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} \
    && rm -rf /tmp/composer-setup.php

CMD ["-"]
ENTRYPOINT ["composer", "--ansi"]