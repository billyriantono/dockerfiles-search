FROM php:apache
RUN apt-get update && apt-get install -y libpng-dev libjpeg-dev libpq-dev && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install gd
RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql
RUN docker-php-ext-install pdo pdo_pgsql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo pdo_mysql
