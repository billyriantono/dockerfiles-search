FROM php:7-fpm

MAINTAINER Nick Lee <nicholaslee1990@hotmail.com>

# install php modules
RUN apt-get update && apt-get install -y --force-yes \
    freetds-dev \
    libicu-dev \
    libpq-dev \
    libmcrypt-dev \
    libpng-dev \
    libssl-dev \
    libgmp-dev \
    libxml2-dev \
    git \
    python-pip \
    python-dev \
    build-essential \
 && rm -r /var/lib/apt/lists/* \
 && cp -s /usr/lib/x86_64-linux-gnu/libsybdb.so /usr/lib/ \
 && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
 && docker-php-ext-install \
    gd \
    mbstring \
    mcrypt \
    pcntl \
    pdo_dblib \
    pdo_mysql \
    pdo_pgsql \
    zip \
    soap
    
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get install -y nodejs

# pip, virtualenv, aws
RUN pip install --upgrade pip \
 && pip install awscli --upgrade --user

ENV PATH "~/.local/bin:$PATH"

# composer
COPY php.ini /usr/local/etc/php/
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer