FROM phpplatform/php-apache:7.1

RUN a2enmod rewrite

ENTRYPOINT ["docker-php-entrypoint"]
CMD ["apache2-foreground"]