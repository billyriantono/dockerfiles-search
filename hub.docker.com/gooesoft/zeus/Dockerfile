FROM alpine:3.3



RUN apk --update add \

  nginx \
  curl \
  php-curl \
  php-soap \
  php-zip \
  php-dom \
  php-exif \
  php-phar \
  php-fpm \
  php-fpm \
  php-xml \
  php-pdo \
  php-json \
  php-openssl \
  php-mysql \
  php-pdo_mysql \
  php-mcrypt \
  php-sqlite3 \
  php-pdo_sqlite \
  php-ctype \
  php-zlib \

  git \
  supervisor \
  && rm /var/cache/apk/*

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer


CMD ["crond"]



