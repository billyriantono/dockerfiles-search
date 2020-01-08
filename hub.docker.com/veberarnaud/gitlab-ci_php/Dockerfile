FROM php:7.0-cli
MAINTAINER "VEBER Arnaud <https://github.com/VEBERArnaud>"

# install required packages
RUN buildDeps="git libbz2-dev zlib1g-dev" && \
        set -x && \
        apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/*

# install xdebug extension
RUN pecl install xdebug && \
        docker-php-ext-enable xdebug

# install bcmath2 & zip extensions
RUN installExt="bcmath bz2 zip" && \
        set -x && \
        docker-php-ext-install $installExt

# install composer in $PATH
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer && \
        php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
        chmod +x /usr/local/bin/composer
