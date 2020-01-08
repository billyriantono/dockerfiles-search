FROM tatoonz/nginx-php-fpm

RUN apt-get update \
    && apt-get install -y \
     vim \
     php5-xdebug \
     php5-mysql

RUN usermod -u 1000 www-data
RUN usermod -G staff www-data

COPY ext-xdebug.ini /etc/php5/mods-available/xdebug.ini

VOLUME /unison

RUN sed -i 's/usr\/share\/nginx\/html\/public/unison/g' /etc/nginx/sites-enabled/default
RUN sed -i '3 i\    server_name default;' /etc/nginx/sites-enabled/default

EXPOSE 80