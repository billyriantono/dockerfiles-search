FROM php:7.2

RUN apt-get update \
 && apt-get install -y git vim curl zip unzip

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php composer-setup.php --install-dir=/bin --filename=composer

RUN composer create-project --prefer-dist laravel/laravel /var/www

WORKDIR /var/www

CMD php artisan serve --host=0.0.0.0
