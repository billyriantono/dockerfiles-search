FROM php:7.3-cli-alpine

MAINTAINER Xavier MARCHEGAY <xmarchegay@clever-age.com>

# Add utils
#
RUN apk add vim curl wget git

# Install Composer
#
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

COPY . /app
WORKDIR /app

RUN composer install

COPY . .

CMD ["php", "application.php"]
