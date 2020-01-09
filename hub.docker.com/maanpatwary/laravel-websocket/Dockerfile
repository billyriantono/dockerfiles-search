FROM php:7.2-fpm
# Get repository and install wget and vim
RUN apt-get update && apt-get install --no-install-recommends -y iputils-ping git unzip apt-transport-https
RUN apt-get install --no-install-recommends  -y libgmp-dev re2c libmhash-dev file
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/


RUN docker-php-ext-configure gmp \
    && docker-php-ext-install \
    pdo_mysql \
    pcntl \
    bcmath \
    gmp \
    && docker-php-ext-enable \
            opcache \
    && pecl channel-update pecl.php.net \
    && pecl install ev
# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- \
        --install-dir=/usr/local/bin \
        --filename=composer
# Install supervisor
RUN apt-get install -y \
    cron \
    supervisor

# Memory Limit
RUN echo "memory_limit=2048M" > $PHP_INI_DIR/conf.d/memory-limit.ini
RUN echo "max_execution_time=900" >> $PHP_INI_DIR/conf.d/memory-limit.ini
RUN echo "extension=ev.so" > $PHP_INI_DIR/conf.d/ev.ini
RUN echo "post_max_size=20M" >> $PHP_INI_DIR/conf.d/memory-limit.ini
RUN echo "upload_max_filesize=20M" >> $PHP_INI_DIR/conf.d/memory-limit.ini

# Time Zone
RUN echo "date.timezone=${PHP_TIMEZONE:-UTC}" > $PHP_INI_DIR/conf.d/date_timezone.ini

# Display errors in stderr
RUN echo "display_errors=stderr" > $PHP_INI_DIR/conf.d/display-errors.ini

# Disable PathInfo
RUN echo "cgi.fix_pathinfo=0" > $PHP_INI_DIR/conf.d/path-info.ini

# Disable expose PHP
RUN echo "expose_php=0" > $PHP_INI_DIR/conf.d/path-info.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ADD supervisord.conf /etc/supervisor/conf.d/supervisor.conf
ADD . /var/www/html
WORKDIR /var/www/html




RUN composer install

RUN chmod -R 777 /var/www/html/storage

# CMD ["php-fpm"]

# CMD ["/bin/sh", "-c", "php-fpm -D | tail -f storage/logs/laravel.log"],

# Clean repository
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

CMD /usr/bin/supervisord