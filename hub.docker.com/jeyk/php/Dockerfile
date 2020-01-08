FROM php:7.3-apache-stretch

# Enable Apache modules
RUN a2enmod rewrite

# Use the default production configuration
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

# Add local configuration
COPY php.ini $PHP_INI_DIR/conf.d/php-local.ini

# Install PHP modules
RUN apt-get update \
    && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libbz2-dev \
        libzip-dev \
        imagemagick \
    && docker-php-ext-install iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install bz2 \
    && docker-php-ext-install calendar \
    && docker-php-ext-install exif \
    && docker-php-ext-install gettext \
    && docker-php-ext-install opcache \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install zip

# Install mSMTP to be able to send emails
RUN apt-get install -y msmtp msmtp-mta
COPY msmtprc /etc/

# Fix HTTP/HTTPS issues
COPY fix-https.php /

COPY docker-php-entrypoint /usr/local/bin/
ENTRYPOINT [ "/usr/local/bin/docker-php-entrypoint" ]

CMD ["apache2-foreground"]
