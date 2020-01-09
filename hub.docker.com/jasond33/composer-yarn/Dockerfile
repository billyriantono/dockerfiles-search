FROM alpine:3.6

RUN echo "http://dl-3.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.3/main" >> /etc/apk/repositories

RUN apk upgrade --update && apk --no-cache add git curl php-cli php-openssl php-json php-phar nodejs yarn

RUN [ -e /usr/local/bin/composer.phar ] || \
    curl -sS https://getcomposer.org/installer | php -- --install-dir /usr/local/bin && \
    [ -e /usr/local/bin/composer.phar ] && \
    ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

RUN php -v && node -v && yarn -v && composer -V
