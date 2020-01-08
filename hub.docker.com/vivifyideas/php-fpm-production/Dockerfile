FROM php:7.2-fpm

# Install additional php dependencies
RUN apt-get -y update \
    && apt-get -y install \
    # Install tools
    imagemagick \
    graphicsmagick \
    ghostscript \
    python \
    unzip \
    # Libraries
    libldap-2.4-2 \
    libxslt1.1 \
    zlib1g \
    libpng16-16 \
    # libmcrypt4 \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    # Dev and headers
    libmagickwand-dev \
    libbz2-dev \
    libicu-dev \
    libldap2-dev \
    libldb-dev \
    # libmcrypt-dev \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    libpng-dev \
    # && pecl install mcrypt-1.0.1 \
    && docker-php-ext-configure intl \
    # && docker-php-ext-enable mcrypt\
    && export CFLAGS="$PHP_CFLAGS" CPPFLAGS="$PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS" \
    && pecl install imagick-3.4.3 \
    && docker-php-ext-enable imagick \
    && docker-php-ext-configure gd \
    --with-freetype-dir=/usr/lib/ \
    --with-png-dir=/usr/lib/ \
    --with-jpeg-dir=/usr/lib/ \
    && docker-php-ext-install \
    bcmath \
    bz2 \
    calendar \
    exif \
    intl \
    gettext \
    mysqli \
    hash \
    pcntl \
    pdo_mysql \
    soap \
    sockets \
    tokenizer \
    sysvmsg \
    sysvsem \
    sysvshm \
    shmop \
    xsl \
    zip \
    gd \
    gettext \
    opcache \
    && apt-get purge -y -f --force-yes \
    libbz2-dev \
    libicu-dev \
    libldap2-dev \
    libldb-dev \
    # libmcrypt-dev \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    libpng-dev \
    iputils-ping \
    procps \
    && rm -rf /var/lib/apt/lists/*

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

RUN composer global require hirak/prestissimo
