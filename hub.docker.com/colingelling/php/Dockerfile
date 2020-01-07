FROM php:7.3-fpm-alpine3.9

# Environment Variables
ENV COMPOSER_ALLOW_SUPERUSER 1

# Setting up working directory for PHP
WORKDIR /var/www/html

# Mount location where Unix socks will be created
VOLUME /var/lib/php7/

# Updating repo
RUN apk apk update

# Install dependencies
RUN apk update && \
    apk upgrade && \
    apk add --no-cache --update \
    git \
    subversion \
    linux-headers \
    binutils-gold \
    openssh \
    mercurial \
    tini \
    bash \
    patch \
    curl \
    m4 \
    perl \
    wget \
    autoconf \
    libmagic \
    file \
    libgcc \
    libstdc++ \
    binutils \
    php-pear \
    php-intl \
    php-pspell \
    php-recode \
    php-sqlite3 \
    php-tidy \
    php-xmlrpc \
    php-xsl \
    php-gettext \
    php-mbstring \
    php-soap \
    gmp \
    gnupg \
    libgomp \
    libatomic \
    mpfr3 \
    gcc \
    musl-dev \
    libc-dev \
    g++ \
    make \
    re2c \
    libmcrypt-dev \
    icu-dev \
    libxslt-dev \
    zlib-dev \
    dpkg-dev \
    libzip-dev \
    zip \
    libxml2-dev \
    sqlite-dev \
    curl-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype \
    libpng \
    libjpeg-turbo \
    libjpeg-turbo-dev \
    libedit-dev \
    npm \
    yarn \
    freetype-dev && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/*

# Configure PHP extensions
RUN docker-php-ext-configure json && \
    docker-php-ext-configure session && \
    docker-php-ext-configure zip --with-libzip && \
    docker-php-ext-configure ctype && \
    docker-php-ext-configure tokenizer && \
    docker-php-ext-configure simplexml && \
    docker-php-ext-configure dom && \
    docker-php-ext-configure mbstring && \
    docker-php-ext-configure zip && \
    docker-php-ext-configure pdo && \
    docker-php-ext-configure pdo_sqlite && \
    docker-php-ext-configure pdo_mysql && \
    docker-php-ext-configure curl && \
    docker-php-ext-configure iconv && \
    docker-php-ext-configure xml && \
    docker-php-ext-configure phar && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Build and install PHP extensions
RUN docker-php-ext-install json \
    session \
    ctype \
    tokenizer \
    simplexml \
    dom \
    mbstring \
    zip \
    pdo \
    pdo_sqlite \
    pdo_mysql \
    curl \
    iconv \
    xml  \
    phar \
    gd \
    readline \
    soap \
    mysqli \
    json \
    xsl \
    bcmath

# Copy php environment file from image to container
COPY conf.d/php.ini /usr/local/etc/php/conf.d/php.ini

RUN docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/

RUN apk add --no-cache --virtual .build-deps zlib-dev \
 && docker-php-ext-install zip \
 && runDeps="$( \
    scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
    | tr ',' '\n' \
    | sort -u \
    | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
    )" \
 && apk add --virtual .composer-phpext-rundeps $runDeps \
 && apk del .build-deps

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

# set Composer workdirectory
WORKDIR /app

# Expose gateway port
EXPOSE 9000