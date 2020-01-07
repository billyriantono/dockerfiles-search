FROM ambientum/php:7.1-nginx

WORKDIR /var/www/app

COPY . /var/www/app
RUN sudo chmod 777 -R . && composer install
RUN php artisan storage:link

EXPOSE 8080
