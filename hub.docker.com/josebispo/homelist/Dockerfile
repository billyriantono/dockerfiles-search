FROM richarvey/nginx-php-fpm:1.5.0


LABEL maintainer="Cristian Mello <cristianc.mello@gmail.com>"

# Dependencies
RUN set -ex && \
    apk --update --no-cache add \
    tzdata \
    nano \
    vim \
    gd \
    parallel \
    freetype \
    libpng \
    libjpeg-turbo \
    freetype-dev \
    libpng-dev \
    jq \
    php7 \
    php7-dom \
    php7-fpm \
    php7-mbstring \
    php7-mcrypt \
    php7-opcache \
    php7-pdo \
    php7-pdo_mysql \
    php7-json \
    php7-dev \
    php7-pear \
    php7-xml \
    php7-xmlwriter \
    php7-xmlrpc \
    php7-xmlreader \
    php7-simplexml \
    php7-soap \
    php7-tokenizer \
    php7-phar \
    php7-openssl \
    php7-json \
    php7-curl \
    php7-ctype \
    php7-session \
    php7-gd \
    php7-zlib \
    nodejs-npm

# Install the mongodb extension
RUN apk update && apk add autoconf g++ gcc make && \
    pecl install mongodb && \
    docker-php-ext-enable mongodb && \
    apk del --purge autoconf g++ gcc make

# NPM installations
RUN npm install -g \
    yarn
