FROM php:5.6.34-apache

RUN apt-get update && apt-get install -y unzip

# Install Composer and PHP Unit
RUN curl -fsSL https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require phpunit/phpunit ^5 --no-progress --no-scripts --no-interaction

ENV PATH /root/.composer/vendor/bin:$PATH