FROM ossinkine/php-xdebug

RUN apk add --no-cache openssl

RUN set -x \
    && wget https://phar.phpunit.de/phpunit-5.7.phar \
    && chmod +x phpunit-5.7.phar \
    && mv phpunit-5.7.phar /usr/local/bin/phpunit
