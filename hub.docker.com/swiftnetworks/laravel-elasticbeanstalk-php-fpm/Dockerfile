FROM php:7.3-fpm

RUN apt-get update && apt-get install -y libpq-dev --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_pgsql pcntl bcmath opcache

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"

COPY opcache.ini /usr/local/etc/php/conf.d/opcache.ini

RUN mv composer.phar /usr/local/bin/composer

RUN usermod -u 1000 www-data
RUN usermod -G staff www-data

COPY compile_and_run.sh /usr/local/bin/compile_and_run.sh

RUN chmod +x /usr/local/bin/compile_and_run.sh

CMD ["/usr/local/bin/compile_and_run.sh"]
