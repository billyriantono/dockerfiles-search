FROM php:7.0-apache

RUN apt-get update && apt-get install -y wget libicu-dev libjpeg-dev libpng-dev libfreetype6-dev && \
    docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install pdo pdo_mysql gd intl zip && \
    a2enmod rewrite

RUN wget https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb
RUN dpkg -i wkhtmltox_0.12.5-1.stretch_amd64.deb; exit 0
RUN apt-get update && apt-get install -f -y
RUN ln -s /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
