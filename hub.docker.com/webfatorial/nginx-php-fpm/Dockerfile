FROM richarvey/nginx-php-fpm

MAINTAINER webfatorial <webfatorial@webfatorial.com>

# Install packages
RUN apk --update --repository http://dl-3.alpinelinux.org/alpine/edge/main add \
    libwebp-dev \
    libxml2 \
    tzdata \
    unzip --repository http://nl.alpinelinux.org/alpine/edge/testing/

RUN docker-php-ext-configure bcmath --enable-bcmath
RUN docker-php-ext-configure intl --enable-intl
RUN docker-php-ext-configure sockets --enable-bcmath
RUN docker-php-ext-configure zip --enable-zip

RUN docker-php-ext-configure gd --with-gd --with-png-dir=/usr --with-jpeg-dir=/usr/lib64
RUN docker-php-ext-configure mbstring --enable-mbstrin
RUN docker-php-ext-install gd
RUN docker-php-ext-install mbstring

RUN docker-php-source delete

# Small fixes and cleanup
RUN ln -s /etc/php7 /etc/php && \
    ln -s /usr/bin/php7 /usr/bin/php && \
    ln -s /usr/sbin/php-fpm7 /usr/bin/php-fpm && \
    ln -s /usr/lib/php7 /usr/lib/php && \
    rm -fr /var/cache/apk/*

# Install wp-cli
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x wp-cli.phar && \
    mv wp-cli.phar /usr/local/bin/wp

# OPcache
RUN echo "opcache.enable = 0"  >> ${php_vars}
RUN echo "opcache.enable_cli = 0"  >> ${php_vars}
RUN echo "opcache.memory_consumption = 1024"  >> ${php_vars}
RUN echo "opcache.max_accelerated_files = 100000"  >> ${php_vars}
RUN echo "opcache.validate_timestamps = 0"  >> ${php_vars}
RUN echo "opcache.enable_file_override = 1"  >> ${php_vars}
RUN echo "opcache.max_waste_percentage = 50"  >> ${php_vars}
RUN echo "opcache.file_cache = /var/www/.opcache"  >> ${php_vars}

# PHP vars
RUN echo "max_input_vars = 10000"  >> ${php_vars}
RUN echo "max_execution_time = 600"  >> ${php_vars}


# Timezone
RUN cp /usr/share/zoneinfo/UTC /etc/localtime && \
    echo "UTC" > /etc/timezone


CMD ["/start.sh"]