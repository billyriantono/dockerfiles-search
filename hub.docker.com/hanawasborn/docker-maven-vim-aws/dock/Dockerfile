# using Debian 9.5
FROM halvardssm/debianbase:latest 
WORKDIR ~
VOLUME laravel/. /var/www/laravel/html/
RUN docker run --rm -v $(pwd):/app composer/composer install
EXPOSE 80
ENV NAME debianbase