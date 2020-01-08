FROM php:7.3

## Container uitbreidingen (nodig voor composer)
RUN apt-get clean && \
    apt-get update -qq && \
    apt-get install -y -qq \
        g++ \
        git \
        imagemagick \
        libicu-dev \
        libmagickwand-dev \
        libxml2-dev \
        libzip-dev \
        locales \
        rsync \
        unzip \
        zlib1g-dev && \
    rm -rf /var/lib/apt/lists/*

## Install dutch locale
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "nl_NL.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

# PHP Extensies toevoegen
RUN docker-php-ext-install bcmath && \
    docker-php-ext-install calendar && \
    docker-php-ext-install soap && \
    docker-php-ext-install zip && \
    docker-php-ext-configure intl && docker-php-ext-install intl && \
    pecl install imagick && docker-php-ext-enable imagick && \
    pecl install pcov && docker-php-ext-enable pcov

# Ini configuraties
RUN echo "date.timezone = Europe/Amsterdam" > /usr/local/etc/php/conf.d/timezone.ini && \
    echo "short_open_tag = off" > /usr/local/etc/php/conf.d/short_open.ini

# Installatie composer
RUN php -r "readfile('https://getcomposer.org/installer');" > composer-setup.php && \
    php composer-setup.php --install-dir=/usr/local/bin/ --filename=composer && \
    php -r "unlink('composer-setup.php');"

# Installatie afhankelijkheden
RUN composer global require hirak/prestissimo

CMD ["php", "-a"]
