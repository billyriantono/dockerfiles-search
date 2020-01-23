FROM php:7.2.19-fpm

MAINTAINER bastard640 <aleksandrzvanko@gmail.com>

ENV TZ=Europe/Moscow PHP_DIR_MODE=770

WORKDIR /var/www

RUN set -ex; \
    rm -rf /tmp/pear; \
    echo "${TZ}" > /etc/timezone; \
    ln -sfn /usr/share/zoneinfo/${TZ} /etc/localtime; \
    \
    apt-get update && apt-get install -y libbz2-dev libxslt-dev libmagickwand-dev libjpeg62-turbo-dev libpng-dev libxml2-dev unzip git gosu msmtp \
    && pecl install -o -f imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install calendar gd opcache iconv mysqli pdo pdo_mysql zip exif gettext pcntl shmop sockets sysvmsg sysvsem sysvshm wddx xsl \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/pear ~/.pearrc

ENV COMPOSER_ALLOW_SUPERUSER=1 COMPOSER_HOME=/tmp/.composer RUN_USER=root

COPY . /tmp/build/

# See https://getcomposer.org/doc/faqs/how-to-install-composer-programmatically.md
RUN set -ex; \
    curl -fso composer-setup.php 'https://getcomposer.org/installer'; \
    curl -fs 'https://composer.github.io/installer.sha384sum' | sha384sum -c -; \
    php composer-setup.php --quiet --no-ansi --install-dir=/usr/local/bin --filename=composer; \
    rm composer-setup.php;

RUN set -ex; \
    mv /tmp/build/www.conf ${PHP_INI_DIR}/../php-fpm.d; \
    mv /tmp/build/docker-entrypoint.sh /opt; \
    mv /tmp/build/php-custom.ini ${PHP_INI_DIR}/conf.d; \
    rm -rf /tmp/build; \
    \
    mkdir -p /var/php/log /var/php/tmp /var/php/sessions /var/php/upload; \
    chown ${PHP_DIR_OWNER}:www-data /var/php/*; \
    chmod ${PHP_DIR_MODE} /var/php/*;

ENTRYPOINT ["/opt/docker-entrypoint.sh"]

VOLUME ["/var/www", "/var/php"]

CMD ["php-fpm"]