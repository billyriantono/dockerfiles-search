FROM php:7-cli

MAINTAINER Christian Daguerre <christian@daguer.re>

ENV TIMEZONE Europe/Paris
ENV PATH $PATH:/var/www/angular/node_modules/.bin

ADD ./php.ini /usr/local/etc/php/conf.d/

# ENV PHP_EXTRA_CONFIGURE_ARGS --enable-opcache --enable-opcache-file --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data

RUN deps=" \
        vim \
        git \
        locales \
    " \
    && apt-get update && apt-get install -y $deps --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# Basic extensions
RUN docker-php-ext-install exif mbstring pdo_mysql opcache pcntl

# Zip
RUN apt-get update && apt-get install -y zlib1g-dev --no-install-recommends \
    && docker-php-ext-install zip \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# Intl
RUN apt-get update && apt-get install -y libicu-dev --no-install-recommends \
    && docker-php-ext-install intl \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# Soap
RUN apt-get update && apt-get install -y libxml2-dev --no-install-recommends \
    && docker-php-ext-install soap \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# APCu & APC BC beta
# RUN pecl install apcu && docker-php-ext-enable apcu \
#     && pecl install apcu_bc-1.0.3 \
#     && echo "extension=apc.so" > $PHP_INI_DIR/conf.d/z-apc.ini

# Memcached
# We need to get the php7 branch of php-memcached from Github
RUN apt-get update && apt-get install -y libmemcached-dev --no-install-recommends \
    && git clone -b php7 --single-branch https://github.com/php-memcached-dev/php-memcached.git /usr/src/php/ext/memcached \
    && (cd /usr/src/php/ext/memcached && git reset --hard 6ace07da69a5ebc021e56a9d2f52cdc8897b4f23) \
    && docker-php-ext-install memcached \
    && find /usr/src/php/ext/memcached -type f -not -name '*.so' | xargs rm \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# Php Redis
# We need to get the php7 branch of phpredis from Github
RUN git clone -b php7 --single-branch https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis\
    && (cd /usr/src/php/ext/redis && git reset --hard 2887ad1130aba5aee029a64140d111544e62d56d)  \
    && docker-php-ext-install redis \
    && find /usr/src/php/ext/redis -type f -not -name '*.so' | xargs rm

# Imagick
# Php7 support isnt stable for imagick so we use the release candidate
RUN apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends \
    && pecl install imagick-3.4.0RC6 && docker-php-ext-enable imagick \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# GD
RUN apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev --no-install-recommends \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# Blackfire
RUN curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/70 \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
    && mv /tmp/blackfire-*.so `php -r "echo ini_get('extension_dir');"`/blackfire.so \
    && echo "extension=blackfire.so\nblackfire.agent_socket=\${BLACKFIRE_PORT}" > $PHP_INI_DIR/conf.d/blackfire.ini

# Nodejs
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash - \
    && apt-get update && apt-get install -y nodejs --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require hirak/prestissimo

# WkhtmltoX
RUN apt-get update && apt-get update && apt-get install -y xfonts-base xfonts-75dpi --no-install-recommends \
    && curl -L -sO http://download.gna.org/wkhtmltopdf/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-jessie-amd64.deb \
    && dpkg -i wkhtmltox-0.12.2.1_linux-jessie-amd64.deb \
    && mv /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf \
    && mv /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage \
    && rm wkhtmltox-0.12.2.1_linux-jessie-amd64.deb \
    && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

RUN echo $TIMEZONE > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

RUN echo '\
      de_DE ISO-8859-1\n\
      de_DE.UTF-8 UTF-8\n\
      de_DE@euro ISO-8859-15\n\
      en_GB ISO-8859-1\n\
      en_GB.ISO-8859-15 ISO-8859-15\n\
      en_US ISO-8859-1\n\
      en_US.ISO-8859-15 ISO-8859-15\n\
      en_US.UTF-8 UTF-8\n\
      fr_FR ISO-8859-1\n\
      fr_FR.UTF-8 UTF-8\n\
      fr_FR@euro ISO-8859-15\n\
      nl_BE ISO-8859-1\n\
      nl_BE.UTF-8 UTF-8\n\
      nl_BE@euro ISO-8859-15\n\
      nl_NL ISO-8859-1\n\
      nl_NL.UTF-8 UTF-8\n\
      nl_NL@euro ISO-8859-15\n' >> /etc/locale.gen \
    && /usr/sbin/locale-gen

RUN usermod -u 1000 www-data

RUN mkdir -p /var/app/logs /var/app/cache && chown -R "www-data":"www-data" /var/app/cache /var/app/logs && chmod -R g+rwx /var/app/logs /var/app/cache

WORKDIR /var/www