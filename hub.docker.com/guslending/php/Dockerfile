FROM alpine:latest

RUN apk add --no-cache php7 \
      php7-bcmath php7-pdo php7-openssl php7-mbstring \
      php7-tokenizer php7-xml php7-ctype php7-json \
      php7-session php7-dom php7-pdo_mysql

RUN apk add --no-cache php7-pecl-xdebug

COPY php.ini /etc/php7/php.ini
COPY php-xdebug.ini /etc/php7/conf.d/xdebug.ini

RUN php -v && php -m

WORKDIR /var/www/app
