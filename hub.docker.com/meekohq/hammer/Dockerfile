FROM php:7.4.0-fpm

LABEL maintainer="damiencriado <damien@damien.id>"

WORKDIR /root

###########################################################################
# Custom Scripts
###########################################################################

COPY ./scripts/apt-get-clean.sh /usr/local/bin/apt-get-clean
RUN chmod +x /usr/local/bin/apt-get-clean

COPY ./scripts/apt-get-install.sh /usr/local/bin/apt-get-install
RUN chmod +x /usr/local/bin/apt-get-install

COPY ./scripts/pecl-install.sh /usr/local/bin/pecl-install
RUN chmod +x /usr/local/bin/pecl-install

###########################################################################
# Base Tools
###########################################################################

RUN apt-get-install gcc make gnupg apt-utils libc6-dev procps

RUN apt-get-install \
    cron \
    htop \
    nano \
    ncdu \
    curl \
    unzip \
    wget \
    git \
    python \
    python-pip \
    && pip install setuptools --no-cache-dir

###########################################################################
# French language pack
###########################################################################

RUN apt-get-install locales \
    && sed -i "s/# fr_FR.UTF-8 UTF-8/fr_FR.UTF-8 UTF-8/g" /etc/locale.gen \
    && /usr/sbin/locale-gen

###########################################################################
# Wkhtmltopdf
###########################################################################

RUN apt-get-install \
    fontconfig \
    libxrender1 \
    libxext6 \
    xfonts-75dpi \
    xfonts-base \
    libjpeg-dev \
    && wget -q https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb \
    && dpkg -i wkhtmltox_0.12.5-1.stretch_amd64.deb \
    && rm wkhtmltox_0.12.5-1.stretch_amd64.deb

###########################################################################
# Image Optimizer
###########################################################################

RUN apt-get-install \
    libjpeg-dev \ 
    libpng-dev \
    jpegoptim \
    optipng \
    pngquant \
    gifsicle

###########################################################################
# NODE
###########################################################################

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash \
    && apt-get install -y nodejs \
    && apt-get-clean \
    && rm /etc/apt/sources.list.d/nodesource.list

###########################################################################
# Browsershot
###########################################################################
RUN apt-get-install gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget\
    && npm install puppeteer --global --unsafe-perm=true \
    && chmod -R o+rx /usr/lib/node_modules/puppeteer/.local-chromium

###########################################################################
# PHP EXTENSION
###########################################################################

# EXTENSION: PDO MySQL
RUN docker-php-ext-install pdo_mysql

# EXTENSION: GD
RUN apt-get-install libfreetype6-dev libjpeg-dev \
    && docker-php-ext-configure gd --with-jpeg --with-freetype \
    && docker-php-ext-install gd

# EXTENSION: Socket
#RUN docker-php-ext-install sockets

# EXTENSION: Calendar
RUN docker-php-ext-install calendar

# EXTENSION: ZIP
RUN apt-get-install libzip-dev \
    && docker-php-ext-install zip

# EXTENSION: SOAP
RUN mv /etc/apt/preferences.d/no-debian-php /tmp/no-debian-php \
    && apt-get-install libxml2-dev php-soap \
    && mv /tmp/no-debian-php /etc/apt/preferences.d/no-debian-php \
    && docker-php-ext-install soap

# EXTENSION: PCNTL
RUN docker-php-ext-install pcntl

# EXTENSION: OPcache
RUN docker-php-ext-install opcache

ENV PHP_OPCACHE_VALIDATE_TIMESTAMPS="0" \
    PHP_OPCACHE_MAX_ACCELERATED_FILES="16229" \
    PHP_OPCACHE_MEMORY_CONSUMPTION="192" \
    PHP_OPCACHE_INTERNED_STRINGS_BUFFER="64" \
    PHP_OPCACHE_MAX_WASTED_PERCENTAGE="10"

COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# EXTENSION: Xdebug
#/usr/local/lib/php/extensions/no-debug-non-zts-20190902/xdebug.so
RUN pecl-install xdebug

# EXTENSION: BCMATH
RUN docker-php-ext-install bcmath

# EXTENSION: EXIF
RUN docker-php-ext-install exif

# EXTENSION: mbstring
RUN apt-get-install libonig-dev \
    && docker-php-ext-install mbstring

# EXTENSION: phpredis
RUN pecl-install redis \
    && docker-php-ext-enable redis

###########################################################################
# Composer
###########################################################################

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('https://composer.github.io/installer.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN composer global require hirak/prestissimo

###########################################################################
# Datadog PHP Tracer
###########################################################################

RUN wget https://github.com/DataDog/dd-trace-php/releases/download/0.36.1/datadog-php-tracer_0.36.1_amd64.deb -O datadog-php-tracer.deb \
    && dpkg -i datadog-php-tracer.deb \
    && rm datadog-php-tracer.deb
ENV DD_TRACE_ENABLED false

###########################################################################
# Finalize
###########################################################################

COPY ./www.conf /usr/local/etc/php-fpm.d/www.conf
COPY ./php.ini /usr/local/etc/php/php.ini

RUN mkdir /app \
    && chown root:root /app

WORKDIR /app
EXPOSE 9000
CMD ["php-fpm", "--allow-to-run-as-root"]
