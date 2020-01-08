FROM php:5.6-apache
RUN apt-get update && apt-get install -y git --no-install-recommends && rm -r /var/lib/apt/lists/*
RUN rm -rf /var/www/html/*
RUN git clone https://github.com/Pyrex-FWI/audio.git /var/www/html/
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin && mv /usr/bin/composer.phar /usr/bin/composer
#COPY audio/ /var/www/html/
RUN chown -R www-data /var/www/html/app/cache/
RUN chown -R www-data /var/www/html/app/logs/
RUN echo "date.timezone = Europe/Paris" >/usr/local/etc/php/php.ini
WORKDIR /var/www/html/
#COPY parameters.yml.dist /var/www/html/app/conf/
RUN composer install -qn
