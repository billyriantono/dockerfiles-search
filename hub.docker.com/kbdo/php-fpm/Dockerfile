FROM php:fpm-alpine

RUN apk --no-cache add shadow && usermod -u 101 www-data && groupmod -g 101 www-data

# install extensions
RUN docker-php-ext-enable opcache  
RUN docker-php-ext-install sockets calendar exif bcmath

# intl, zip, soap, xmlrpc
RUN apk add --update --no-cache libintl icu icu-dev libxml2 libxml2-dev libzip libzip-dev \
    && docker-php-ext-install intl zip soap xmlrpc \
    && apk del --no-cache icu-dev libxml2-dev libzip-dev

# mysqli, pdo, pdo_mysql, pdo_pgsql
RUN apk add --no-cache postgresql-libs postgresql-dev \
    && docker-php-ext-install mysqli pdo_mysql pdo_pgsql \
    && apk del --no-cache postgresql-dev
    
# gmp
RUN apk add --update --no-cache gmp gmp-dev \
    && docker-php-ext-install gmp \
    && apk del --no-cache gmp-dev
    
# php-redis
ENV PHPREDIS_VERSION 5.1.1

RUN docker-php-source extract \
    && curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && docker-php-source delete
    
# git client
# RUN apk add --update --no-cache git

# imagick
RUN apk add --update --no-cache autoconf g++ imagemagick imagemagick-dev libtool make pcre pcre-dev \
    && pecl install imagick \
    && apk del --no-cache autoconf g++ libtool make pcre-dev imagemagick-dev
    
# gettext
RUN apk add --update --no-cache gettext gettext-dev \
    && docker-php-ext-install gettext \
    && apk del --no-cache gettext-dev

# gd
RUN apk add --update --no-cache libpng libpng-dev \
    && docker-php-ext-install gd \
    && apk del --no-cache libpng-dev
    
# xsl
RUN apk add --update --no-cache libxslt libxslt-dev libgcrypt libgcrypt-dev \
    && docker-php-ext-install xsl \
    && apk del --no-cache libxslt-dev libgcrypt-dev
    
# bz2
RUN apk add --update --no-cache bzip2 bzip2-dev \
    && docker-php-ext-install bz2 \
    && apk del --no-cache bzip2-dev

COPY config/. $PHP_INI_DIR/conf.d/

# Use the default production configuration
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

RUN sed -i 's/post_max_size =.*/post_max_size = 50M/g' "$PHP_INI_DIR/php.ini" \
 && sed -i 's/upload_max_filesize =.*/upload_max_filesize = 50M/g' "$PHP_INI_DIR/php.ini" \
 && sed -i 's/;date.timezone =.*/date.timezone = PRC/g' "$PHP_INI_DIR/php.ini" \
 && sed -i 's/short_open_tag =.*/short_open_tag = On/g' "$PHP_INI_DIR/php.ini" \
 && sed -i 's/;cgi.fix_pathinfo=.*/cgi.fix_pathinfo=0/g' "$PHP_INI_DIR/php.ini" \
 && sed -i 's/max_execution_time =.*/max_execution_time = 300/g' "$PHP_INI_DIR/php.ini" \
 && sed -i 's/max_input_time =.*/max_input_time = 300/g' "$PHP_INI_DIR/php.ini" \
 && sed -i 's/expose_php =.*/expose_php = off/g' "$PHP_INI_DIR/php.ini"
 
RUN sed -i 's/;pm.max_requests = .*/pm.max_requests = 500/g' "$PHP_INI_DIR/../php-fpm.d/www.conf" \
    && sed -i 's/;request_terminate_timeout = .*/request_terminate_timeout = 15m/g' "$PHP_INI_DIR/../php-fpm.d/www.conf" \
    && sed -i 's/;pm.max_requests = .*/pm.max_requests = 500/g' "$PHP_INI_DIR/../php-fpm.d/www.conf"
