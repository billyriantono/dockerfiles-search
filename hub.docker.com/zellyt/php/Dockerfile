FROM php:7.2-fpm
LABEL maintainer="Zellyt IT <it@zellyt.com>"

# Adding magento required extensions
RUN apt-get update && apt-get install -y \
        wget \
        unzip \
        zlib1g-dev \
        libicu-dev \
        g++ \
        libxml2-dev \
        libxslt-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd \
        --with-jpeg-dir=/usr/include/ \
        --with-freetype-dir=/usr/lib/x86_64-linux-gnu \
    && docker-php-ext-install gd intl soap xsl zip bcmath pdo_mysql \
    && docker-php-ext-enable opcache

# Adding magento php configuration
COPY files/config/php.ini $PHP_INI_DIR/

EXPOSE 9000
CMD ["php-fpm"]