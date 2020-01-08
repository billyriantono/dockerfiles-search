FROM wiwatsrt/docker-laravel-php:7.3
   
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer 

WORKDIR /var/www

RUN composer self-update

ENTRYPOINT ["composer"]

CMD ["--help"]
