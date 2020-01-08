FROM php:7.1-fpm

MAINTAINER Jordan Hinkle mozziter@gmail.com

ENV APPLICATION_DIRECTORY=/var/www/html \
    PHPREDIS_VERSION=3.1.1

ADD usr/local/bin/ /usr/local/bin

RUN \
    apt-get update \
    && apt-get install -y \
        cron \
        libfreetype6-dev \
        libicu-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpcre3-dev \
        libpng12-dev \
        libtidy-dev \
        libxml2-dev \
        libxslt-dev \
        gettext \
        --no-install-recommends \

    && echo "\n##### Install pecl-based extensions" \
    && pecl install \
        redis-$PHPREDIS_VERSION \

    && echo "\n##### Configure php extensions" \
    && docker-php-ext-configure \
        gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \

    && echo "\n##### Install core/other PHP extensions" \
    && docker-php-ext-install \
        gd \
        intl \
        mcrypt \
        mysqli \
        pdo_mysql \
        sockets \
        tidy \
        zip \

    && echo "\n##### Enable PHP extensions" \
    && docker-php-ext-enable \
        redis \

    && echo "\n##### Install Composer" \
    && curl -sS https://getcomposer.org/installer  | php -- --install-dir=/usr/local/bin --filename=composer \

    && echo "\n##### Install WP CLI" \
    && curl https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar -o /tmp/wp-cli.phar \
    && mv /tmp/wp-cli.phar /usr/local/bin/wp-cli.phar \
    && chmod +x /usr/local/bin/wp-cli.phar \
    && chmod +x /usr/local/bin/wp \

    && echo "\n##### Set owner" \
    && chown -R www-data:www-data $APPLICATION_DIRECTORY \
    
    && echo "##### Image cleanup" \
    && apt-get clean autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* \
    && chown -R www-data:www-data /tmp \

    && echo "##### Setting up www-data" \
    && mkdir -p /home/www-data/.composer  \
    && chown -R www-data:www-data /home/www-data \
    && usermod -d /home/www-data www-data