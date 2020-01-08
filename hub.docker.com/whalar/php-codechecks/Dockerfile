FROM php:7.1-cli-stretch

ENV BUILD_DEPS \
    build-essential \
    libzip-dev \
    libsasl2-dev \
    libssl-dev \
    zlib1g-dev \
    git \
    zip

# install system dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends ${BUILD_DEPS} \
    # install composer
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    # install php extensions
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install \
        zip \
    # remove
    && rm -rf /var/lib/apt/lists/*
