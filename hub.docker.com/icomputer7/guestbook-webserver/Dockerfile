FROM php:apache

RUN docker-php-ext-install mysqli

COPY src /var/www/html

EXPOSE 80

CMD ["apache2-foreground"]