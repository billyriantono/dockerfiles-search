FROM php:apache
RUN apt-get update && apt-get install -y libxslt-dev && docker-php-ext-install xsl
RUN apt-get update && apt-get install -y default-mysql-client && docker-php-ext-install mysqli
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd
RUN a2enmod rewrite