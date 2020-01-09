FROM psaudio/alpine-base

WORKDIR /usr/src

#download PHP source
COPY php-7.0.25.tar.gz /usr/src/

# create www-data user and group
RUN set -xe \
    && addgroup -g 82 -S www-data \
    && adduser -u 82 -D -S -G www-data www-data

# install packages needed by PHP during runtime
RUN set -xe \
    && apk add --update --no-cache --virtual .run-dependencies \
        libxml2-dev \
        openssl \
        curl

# build and install PHP
RUN set -xe \
    # extract PHP source
    && tar -xzvf php-7.0.25.tar.gz \
    && cd /usr/src/php-7.0.25/ \
    \
    # install packages needed to build PHP
    && apk add --update --no-cache --virtual .build-dependencies \
        autoconf \
        build-base \
        dpkg \
        dpkg-dev \
        openssl-dev \
        curl-dev \
    \
    # configure PHP build options
    && gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
    && ./configure \
        --build="$gnuArch" \
        --with-openssl \
        --with-zlib \
        --enable-mbstring \
        --with-curl \
    \
    # install PHP
    && make -j$(nproc) \
    && make install \
    \
    # cleanup to reduce image size
    && cd /usr/src/ \
    && rm -rf /usr/src/php-7.0.25/ /usr/src/php-7.0.25.tar.gz \
    && apk del .build-dependencies \
    && rm -rf /var/cache/apk/*

# install Composer
RUN set -xe \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/bin/composer

WORKDIR /app/

ENTRYPOINT ["composer"]