FROM php:7.2-fpm-buster

RUN apt-get update && apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libzip-dev \
        nginx \
        wget \
        nano \
        git \
        unzip \ 
        supervisor \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && usermod -u 1000 www-data
RUN docker-php-ext-configure opcache --enable-opcache \
&& docker-php-ext-install opcache

RUN pecl install zip-1.15.4 \
    && pecl install apcu-5.1.17 \
    && pecl install redis-4.0.1 \
    && pecl install xdebug-2.6.0 \
    && docker-php-ext-enable zip apcu redis xdebug

RUN docker-php-ext-install pdo pdo_mysql

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
&& curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
# Make sure we're installing what we think we're installing!
&& php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
&& php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot \
&& rm -f /tmp/composer-setup.*

# Use the default production configuration + set config voor opcache and apcu
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" && \
  { \
      echo 'zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20170718/opcache.so'; \
      echo 'opcache.memory_consumption=256'; \
      echo 'opcache.interned_strings_buffer=8'; \
      echo 'opcache.max_accelerated_files=8000'; \
      echo 'opcache.revalidate_freq=60'; \
      echo 'opcache.fast_shutdown=1'; \
      echo 'opcache.enable_cli=1'; \
      echo 'opcache.enable=1'; \
  } > /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini && \
  { \
      echo 'extension=apcu.so'; \
      echo 'apc.shm_size=128M'; \
      echo 'apc.num_files_hint=8000'; \
      echo 'apc.ttl=3600'; \
} > /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini

EXPOSE 8080

COPY site.conf /etc/nginx/sites-available/default
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY shopware.conf /etc/nginx/
COPY www.conf /usr/local/etc/php-fpm.d/www.conf
RUN usermod -s /bin/bash www-data
CMD ["/usr/bin/supervisord"]