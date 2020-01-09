FROM shawnoy/php-fpm:7.3.0

LABEL maintainer "shawnoy@outlook.com"

RUN apk --no-cache add libzip-dev && \
    docker-php-ext-install zip

RUN composer global require laravel/installer

ENV PATH $PATH:/root/.composer/vendor/bin

EXPOSE 8080

CMD php artisan serve --host=0.0.0.0 --port=8080
