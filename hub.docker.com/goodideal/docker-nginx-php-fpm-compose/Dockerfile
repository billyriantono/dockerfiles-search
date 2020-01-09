FROM richarvey/nginx-php-fpm:latest

RUN mkdir -p /var/www/html/ \ 
    && curl https://getcomposer.org/composer.phar -o /var/composer.phar \
    && ls -al /var/
    
WORKDIR /var/www/html/
