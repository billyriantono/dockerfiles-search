FROM php:7.0-apache
MAINTAINER Nitra

RUN apt-get update \
    && apt-get install -y \
        curl \
        git \
        zlib1g-dev \
        npm \
        nodejs-legacy

RUN npm install -g bower \
    && npm install -g uglifycss

# For composer and zlib1g-dev also for this module
RUN docker-php-ext-install zip && \
    docker-php-ext-install pdo_mysql        

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY . /var/www
WORKDIR /var/www

CMD ["apache2-foreground"]
