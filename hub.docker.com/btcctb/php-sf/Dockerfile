FROM btcctb/php:7.0

RUN apt-get update

# pour ext intl
RUN apt-get install -y libicu-dev \
 && docker-php-ext-install intl

# pour ext opcache
RUN docker-php-ext-install opcache

# Symfony installer
RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony \
 && chmod a+x /usr/local/bin/symfony

# Configure apache
RUN sed -i 's!/var/www/html!/var/www/web!g' /etc/apache2/sites-enabled/000-default.conf \
 && mv /var/www/html /var/www/web

WORKDIR /var/www
