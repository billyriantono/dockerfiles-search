FROM jenkinsci/blueocean

USER root
# ADD SDK AND BASIC TOOLS.
RUN apk add --update alpine-sdk sudo git bash nano curl gettext

# trust this project public key to trust the packages.
ADD https://php.codecasts.rocks/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub

# make sure you can use HTTPS
RUN apk --update add ca-certificates
ENV ALPINE_VERSION=3.8

# PHP and composer installation
# CONFIGURE ALPINE REPOSITORIES AND PHP BUILD DIR.
RUN echo "http://dl-cdn.alpinelinux.org/alpine/v${ALPINE_VERSION}/main" > /etc/apk/repositories && \
    echo "http://dl-cdn.alpinelinux.org/alpine/v${ALPINE_VERSION}/community" >> /etc/apk/repositories && \
    echo "@php https://php.codecasts.rocks/v${ALPINE_VERSION}/php-7.2" >> /etc/apk/repositories

RUN apk add --update \
    postgresql-client \
    php@php \
    php-mbstring@php \
    php-dev@php \
    php-common@php \
    php-bcmath@php \
    php-bz2@php \
    php-ctype@php \
    php-curl@php \
    php-exif@php \
    php-gd@php \
    php-gmp@php \
    php-iconv@php \
    php-intl@php \
    php-json@php \
    php-mbstring@php \
    php-opcache@php \
    php-openssl@php \
    php-pcntl@php \
    php-pdo@php \
    php-pdo_mysql@php \
    php-pdo_pgsql@php \
    php-pgsql@php \
    php-phar@php \
    php-posix@php \
    php-session@php \
    php-sockets@php \
    php-xmlreader@php \
    php-xml@php \
    php-xmlrpc@php \
    php-xsl@php \
    php-zip@php \
    php-zlib@php \
    php-dom@php \
    php-redis@php \
    php-sodium@php \
    && ln -s /usr/bin/php7 /usr/bin/php \
    && rm -rf /var/cache/apk/*
COPY ./php.ini /etc/php7/php.ini
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# install docker-compose
RUN apk add --no-cache python3 && pip3 install docker-compose

# adding nodejs
RUN apk add --update nodejs nodejs-npm

# install kubectl support for jenkins image
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x kubectl && mv kubectl /bin/kubectl

# cleanup
RUN rm -rf /var/cache/apk/*
