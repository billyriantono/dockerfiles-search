FROM alpine:3.5

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apk update && \
    apk upgrade && \
    rm -frv /var/cache/apk/*

RUN apk add --no-cache \
        \
        # binaries
        curl \
        pcre \
        \
        # php 7
        php7 \
        php7-curl \
        php7-iconv \
        php7-json \
        php7-mbstring \
        php7-openssl \
        php7-phar \
        php7-zip \
        php7-zlib \
        && \
    ln -s /usr/bin/php7 /usr/bin/php && \
    rm -frv /var/cache/apk/*

# Composer installation

RUN \
    mkdir /tmp/composer && \
    curl \
        -o /tmp/composer/composer-setup.php \
        https://getcomposer.org/installer \
    && \
    curl \
        -o /tmp/composer/composer-setup.sig \
        https://composer.github.io/installer.sig \
    && \
    php -r \
        "if (\
            hash(\
                'SHA384',\
                file_get_contents('/tmp/composer/composer-setup.php')\
            ) !== trim(\
                file_get_contents('/tmp/composer/composer-setup.sig')\
            )\
        ) {\
            unlink('/tmp/composer/composer-setup.php');\
            echo 'Invalid installer' . PHP_EOL; exit(1);\
        }"\
    && \
    php /tmp/composer/composer-setup.php \
        --install-dir=/usr/local/bin \
        --filename=composer \
    && \
    composer selfupdate && \
    rm -frv /tmp/composer

ENV PATH /root/.composer/vendor/bin:$PATH

VOLUME ["/app"]
WORKDIR /app
ENTRYPOINT ["composer"]
CMD ["list"]
