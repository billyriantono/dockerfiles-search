# PHP Version
ARG PHP_VERSION
# V8 install flag for base image
ARG INSTALL_V8=false

# Image if V8 doesn't need to be installed
# Will be stripped out by the end of the build
FROM php:${PHP_VERSION}-fpm-alpine as v8-source-false

# Dummy folder to avoid ONBUILD COPY errors
RUN mkdir -p /opt/v8

# Image if V8 should be installed
FROM liquidfish/v8-alpine as v8-source-true

# Dummy image to emulate IF/ELSE with Docker
# "This isn't even my final form!"
FROM v8-source-${INSTALL_V8} as v8-build

# This is the final image
FROM php:${PHP_VERSION}-fpm-alpine

# Copy composer in from child images
COPY --from=composer /usr/bin/composer /usr/bin/composer

ONBUILD ARG INSTALL_V8=false
ONBUILD ARG INSTALL_BCMATH
ONBUILD ARG INSTALL_EXIF
ONBUILD ARG INSTALL_GD
ONBUILD ARG INSTALL_IMAGICK
ONBUILD ARG INSTALL_INTL
ONBUILD ARG INSTALL_MCRYPT
ONBUILD ARG INSTALL_MYSQL
ONBUILD ARG INSTALL_PGSQL
ONBUILD ARG INSTALL_REDIS
ONBUILD ARG INSTALL_XDEBUG
ONBUILD ARG INSTALL_ZIP
ONBUILD ARG DEPS

# Copy V8 if it exists
COPY --from=v8-build /opt/v8 /opt/v8

ONBUILD RUN \
    if [ "$INSTALL_BCMATH" != "false" ]; then \
        export EXT_INSTALL="${EXT_INSTALL} bcmath" \
    ; fi \
    && if [ "$INSTALL_EXIF" = "true" ]; then \
        export DEPS="${DEPS} exiftool" \
        && export EXT_INSTALL="${EXT_INSTALL} exif" \
    ; fi \
    && if [ "$INSTALL_GD" = "true" ]; then \
        export EXT_INSTALL="${EXT_INSTALL} gd" \
        && export BUILD_DEPS="${BUILD_DEPS} freetype-dev libjpeg-turbo-dev libpng-dev libwebp-dev" \
        && export DEPS="${DEPS} freetype libjpeg-turbo libpng libwebp" \
    ; fi \
    && if [ "$INSTALL_IMAGICK" = "true" ]; then \
        export BUILD_DEPS="${BUILD_DEPS} imagemagick-dev" \
        && export DEPS="${DEPS} imagemagick" \
        && PECLS="${PECLS} imagick" \
        && EXT_ENABLE="${EXT_ENABLE} imagick" \
    ; fi \
    && if [ "$INSTALL_INTL" = "true" ]; then \
        export BUILD_DEPS="${BUILD_DEPS} icu-dev" \
        && export DEPS="${DEPS} icu" \
        && EXT_INSTALL="${EXT_INSTALL} intl" \
    ; fi \
    && if [ "$INSTALL_MCRYPT" = "true" ]; then \
        export BUILD_DEPS="${BUILD_DEPS} libmcrypt-dev" \
        && export DEPS="${DEPS} libmcrypt" \
        && EXT_INSTALL="${EXT_INSTALL} mcrypt" \
    ; fi \
    && if [ "$INSTALL_MYSQL" != "false" ]; then \
        export EXT_INSTALL="${EXT_INSTALL} mysqli pdo_mysql" \
    ; fi \
    && if [ "$INSTALL_PGSQL" = "true" ]; then \
        export EXT_INSTALL="${EXT_INSTALL} pgsql pdo_pgsql" \
        && export BUILD_DEPS="${BUILD_DEPS} postgresql-dev" \
        && export DEPS="${DEPS} postgresql-client postgresql-libs" \
    ; fi \
    && if [ "$INSTALL_REDIS" = "true" ]; then \
        export PECLS="${PECLS} redis" \
        && export EXT_ENABLE="${EXT_ENABLE} redis" \
    ; fi \
    && if [ "$INSTALL_XDEBUG" = "true" ]; then \
        export PECLS="${PECLS} xdebug" \
        && export EXT_ENABLE="${EXT_ENABLE} xdebug" \
    ; fi \
    && if [ "$INSTALL_V8" = "true" ]; then \
        export BUILD_DEPS="${BUILD_DEPS} git" \
        && export DEPS="${DEPS} libgcc libstdc++" \
        && export EXT_ENABLE="${EXT_ENABLE} v8js" \
    ; fi \
    && if [ "$INSTALL_ZIP" = "true" ]; then \
        export BUILD_DEPS="${BUILD_DEPS} libzip-dev" \
        && export DEPS="${DEPS} libzip zip" \
        && export EXT_INSTALL="${EXT_INSTALL} zip" \
    ; fi \
    && set -x \
    && apk add --virtual .build-deps $BUILD_DEPS $PHPIZE_DEPS \
    && apk add $DEPS fcgi nginx s6 \
    && if [ "$INSTALL_GD" = "true" ]; then \
        docker-php-ext-configure gd \
    ; fi \
    && if [ "$INSTALL_V8" = "true" ]; then \
        git clone --depth 1 --single-branch --progress --verbose https://github.com/phpv8/v8js.git /tmp/v8js \
        && cd /tmp/v8js \
        # Checkout the proper branch
        && git checkout php7 \
        # Create PHP build environment
        && phpize \
        # Configure
        && ./configure --with-v8js=/opt/v8 \
        # Build the extension
        && NO_INTERACTION=1 \
        && make -j"$(nproc)" \
        # Sanity check during build process.
        && make -j"$(nproc)" test \
        # Install the extension
        && make -j"$(nproc)" install \
        && cd - \
    ; fi \
    && if [ "$INSTALL_ZIP" = "true" ]; then \
        docker-php-ext-configure zip \
    ; fi \
    && if [ -n "$EXT_INSTALL" ]; then \
        docker-php-ext-install -j"$(nproc)" $EXT_INSTALL \
    ; fi \
    && if [ -n "$PECLS" ]; then \
        pecl install $PECLS \
    ; fi \
    && if [ -n "$EXT_ENABLE" ]; then \
        docker-php-ext-enable $EXT_ENABLE \
    ; fi \
    && apk del .build-deps \
    && rm -rf /tmp/* /var/cache/apk/* \
    && cd "$PHP_INI_DIR" \
    && sed -ri \
        -e 's/;(ping\.path)/\1/' \
        ../php-fpm.d/www.conf \
    && ln -s php.ini-production php.ini \
    && sed -ri \
        -e 's/^(expose_php).*$/\1 = Off/' \
        php.ini-production \
    && mkdir /run/nginx

