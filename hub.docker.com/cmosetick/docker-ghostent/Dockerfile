FROM php:7.1-fpm-alpine
RUN apk add --no-cache \
  autoconf \
  gcc \
  make \
  openssl-dev \
  libpng-dev \
  libxml2-dev \
  alpine-sdk \
  gettext-dev \
  pcre-dev \
  libxslt-dev \
  libjpeg-turbo-dev \
  libpng-dev \
&& docker-php-ext-configure gd \
  --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install \
  gd \
  mysqli \
  opcache \
  zip \
  calendar \
  exif \
  gettext \
  pcntl \
  shmop \
  sockets \
  sysvmsg \
  sysvsem \
  sysvshm \
  xsl \
  wddx \
  pdo_mysql \
&& apk del \
  autoconf \
  gcc \
  make \
  openssl-dev \
  alpine-sdk \
  libxml2-dev

ENTRYPOINT ["docker-php-entrypoint"]
EXPOSE 9000

CMD ["php-fpm"]
