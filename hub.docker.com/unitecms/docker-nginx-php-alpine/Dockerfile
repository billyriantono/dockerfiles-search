#
# Unite Alpine Nginx / PHP-FPM image
#

FROM alpine:3.9

LABEL maintainer="Stefan Kamsker<stefan@unite.co.at>"

ENV NAME="alpin-nginx-php" \
    APP_ROOT=/app \
    PATH=/app/bin:$PATH \
    SUMMARY="Unite Nginx / PHP FPM image" \
    DESCRIPTION="Unite Nginx / PHP FPM image"

# add new repo, bash mode
RUN echo 'http://dl-cdn.alpinelinux.org/alpine/v3.9/community' >> /etc/apk/repositories

# install packages
RUN apk --update add \
  --no-cache shadow sudo \
  nginx \
  bash \
  vim \
  php-fpm \
  php-pdo \
  php-zip \
  php-ctype \
  php-iconv \
  php-xmlwriter \
  php-session \
  php-json \
  php-cli \
  php-pdo_mysql \
  php-simplexml \
  php-tokenizer \
  php-bcmath \
  php-zlib \
  php-phar \
  php-curl \
  php-mysqlnd \
  php-xml \
  php-gd \
  php-mbstring \
  php-opcache \
  php-intl \
  php-bcmath \
  php-dom \
  php-fileinfo \
  curl \
  git \
  nodejs-current \
  yarn \
  supervisor

# create user and set workdir
RUN addgroup -g 1122 -S appgroup && adduser -S -G appgroup appuser
WORKDIR ${APP_ROOT}

# install composer & phpunit
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# copy files
COPY ./root/ /

#COPY ./test/index.php /app/public/index.php

# create process and log folders, fix permissions
RUN /usr/bin/container-setup

# clean up to reduce image size
RUN rm -rf /var/cache/apk/*

USER appuser

ENTRYPOINT ["/usr/bin/container-entrypoint"]

CMD ["supervisord", "-n"]
