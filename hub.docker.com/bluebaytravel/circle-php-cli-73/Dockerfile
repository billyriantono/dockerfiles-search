FROM php:7.3.4-cli

RUN apt-get update && \
    apt-get -y -qq install \
    apt-transport-https \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libjpeg-dev \
    libwebp-dev \
    libxpm-dev \
    libpng-dev \
    libzip-dev \
    curl \
    gnupg
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

RUN echo "memory_limit=2048M" > $PHP_INI_DIR/conf.d/memory-limit.ini
RUN apt-get -y install git libsqlite3-dev libxml2-dev unzip yarn zlib1g-dev libpng-dev
RUN docker-php-ext-configure gd \
    --with-gd \
    --with-webp-dir \
    --with-jpeg-dir \
    --with-png-dir \
    --with-zlib-dir \
    --with-xpm-dir \
    --with-freetype-dir
RUN docker-php-ext-install bcmath pcntl pdo pdo_sqlite pdo_mysql soap zip gd exif
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
RUN composer global require "hirak/prestissimo:^0.3"
