FROM josesieiroaltia/workshop-php:7.2-dev

RUN docker-php-ext-install pcntl
COPY ./application /application
RUN composer install
