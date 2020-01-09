FROM        php:7.1-fpm

MAINTAINER  eurekacachetdev@gmail.com

RUN apt-get update && apt-get install -y \
        git cron curl \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        mysql-client \
        libgmp-dev \
        libpq-dev \
    && ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h \
    && docker-php-ext-install -j$(nproc) iconv mcrypt mbstring zip pdo_mysql pdo pdo_pgsql bcmath gmp \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-enable bcmath \
    && docker-php-ext-configure gmp

# install wkhtmltopdf
RUN         apt-get update && \
            apt-get install -y xvfb libfontconfig wkhtmltopdf

# install supervisor
RUN         apt-get install -y supervisor && \
            mkdir -p /var/log/supervisor

# install composer
RUN         curl -sS https://getcomposer.org/installer | /usr/local/bin/php -- --install-dir=/usr/local/bin --filename=composer


# Install Node.js
# RUN         apt-get install -y build-essential

# RUN         curl -sL https://deb.nodesource.com/setup_8.x | bash -

# RUN         apt-get install -y nodejs

RUN         apt-get update \
            && apt-get -y autoremove && apt-get clean \
            && rm -rf /var/lib/apt/lists/*
