FROM php:fpm-alpine

ENV BUILD_DEPS="cmake icu-dev freetype-dev libjpeg-turbo-dev libpng-dev libzip-dev imagemagick-dev gettext-dev" \
    RUN_DEPS="libarchive-tools icu gettext jq zip git figlet wget \
            freetype libjpeg-turbo libpng libzip ruby-full npm composer python g++ mysql-client imagemagick \
            ca-certificates shadow bash"

RUN set -x \
# ---- Installing Build dependencies ----
    && apk --update add --no-cache --virtual .build-deps ${PHPIZE_DEPS} ${BUILD_DEPS} \
# ---- Installing PHP Extension: gd zip intl gettext mysqli pdo_mysql exif ----
    && docker-php-ext-configure gd --with-gd --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-freetype-dir=/usr/include/ --enable-gd-jis-conv \
    && docker-php-ext-configure zip --with-libzip \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-install -j${NPROC} \
        intl gettext mysqli pdo_mysql exif gd zip \
    && (rm -rf /usr/local/lib/php/test/gd || true) \
    && (rm -rf /usr/local/lib/php/doc/gd || true) \
# ---- Update PHP pecl ----
    && pecl channel-update pecl.php.net \
# ---- Installing PHP Extension: imagick ----
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && (rm -rf /usr/local/lib/php/test/imagick || true) \
    && (rm -rf /usr/local/lib/php/doc/imagick || true) \
# ---- Installing PHP Extension: xdebug ----
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && (rm -rf /usr/local/lib/php/test/xdebug || true) \
    && (rm -rf /usr/local/lib/php/doc/xdebug || true) \
# ---- Removing Build dependencies ----
    && apk del .build-deps \
# ---- Installing Running dependencies ----
    && apk --update add ${RUN_DEPS} \
    && update-ca-certificates

# ---- Installing Running env ----
RUN set -x \
    && npm i npm@latest -g \
    && npm install -g grunt-cli webpack-cli \
    && composer self-update \
    && gem install sass -v 3.4.25 \
    && composer global require hirak/prestissimo

COPY ./presetup /usr/local/bin
COPY ./php.ini /usr/local/etc/php/
RUN chmod +x /usr/local/bin/presetup

# Set work directory to the web host path
WORKDIR /var/www

# Run the configsetup file on container start
ENTRYPOINT ["/usr/local/bin/presetup"]
CMD ["php-fpm"]
