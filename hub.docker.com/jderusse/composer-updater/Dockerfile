FROM alpine:edge

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

WORKDIR /srv

# PHP
RUN apk add --no-cache \
        php7 \
 && ln -s /usr/bin/php7 /usr/bin/php

# Performances matter
RUN apk add --no-cache \
        php7-opcache \
        php7-apcu@testing

# Composer
RUN apk add --no-cache \
        php7-zip \
        php7-phar \
        php7-curl \
        php7-zlib \
        php7-mbstring \
        php7-iconv \
        php7-json \
        php7-posix \
        php7-openssl

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
 && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('https://composer.github.io/installer.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
 && php composer-setup.php --install-dir /usr/bin --filename composer \
 && php -r "unlink('composer-setup.php');" \
 && composer -V

RUN echo "memory_limit = -1" >> /etc/php7/conf.d/composer.ini

# Git
RUN apk add --no-cache \
        git \
        openssh-client

RUN git config --global user.email "ci@aptus.ninja" \
 && git config --global user.name "CI"

ENV REMOTE_BRANCH=master
COPY bin/entrypoint /usr/bin/entrypoint

ENTRYPOINT ["entrypoint"]
