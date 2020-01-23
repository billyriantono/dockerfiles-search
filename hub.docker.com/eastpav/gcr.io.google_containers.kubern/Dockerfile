FROM rolandocaldas/workshop-php:7.2-dev

RUN docker-php-ext-install pcntl

COPY ./application /application

RUN php -d memory_limit=-1 /usr/local/bin/composer install