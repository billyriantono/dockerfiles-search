FROM php:7.2-cli-alpine3.8

ENV XDEBUG_VERSION 2.6.1
ENV JPEGOPTIM_URL https://github.com/tjko/jpegoptim/archive/RELEASE.1.4.6.tar.gz
ENV OPTIPNG_URL https://downloads.sourceforge.net/project/optipng/OptiPNG/optipng-0.7.7/optipng-0.7.7.tar.gz
ENV PNGQUANT_URL http://pngquant.org/pngquant-2.12.0-src.tar.gz
ENV GIFSICLE_URL https://github.com/kohler/gifsicle/archive/v1.91.tar.gz

# Install phpize build dependencies
# hadolint ignore=SC2086,DL3018
RUN apk add --no-cache --virtual .phpize-build-deps \
    ${PHPIZE_DEPS}

# Install build dependencies
RUN apk add --no-cache --virtual .build-deps \
    automake=1.16.1-r0 \
    bash=4.4.19-r1 \
    icu-dev=60.2-r2 \
    postgresql-dev=10.5-r0 \
    libjpeg-turbo-dev=1.5.3-r4 \
    libpng-dev=1.6.34-r1

SHELL ["/bin/bash", "-o", "pipefail", "-e", "-x", "-c"]

# Build
RUN docker-php-ext-install \
        bcmath \
        gd \
        intl \
        pdo_pgsql \
    && pecl install \
        grpc \
        redis \
        xdebug-"${XDEBUG_VERSION}" \
    && docker-php-ext-enable \
        grpc \
        redis

# Install jpegoptim
WORKDIR /usr/src/jpegoptim

RUN curl -sSL "${JPEGOPTIM_URL}" | tar -xz -C /usr/src/jpegoptim --strip-components 1 \
    && ./configure \
    && make \
    && make strip \
    && make install \
    && rm -rf /usr/src/jpegoptim

# Install optipng
WORKDIR /usr/src/optipng

RUN curl -sSL "${OPTIPNG_URL}" | tar -xz -C /usr/src/optipng --strip-components 1 \
    && ./configure \
    && make \
    && make install \
    && rm -rf /usr/src/optipng

# Install pngquant
WORKDIR /usr/src/pngquant

RUN curl -sSL "${PNGQUANT_URL}" | tar -xz -C /usr/src/pngquant --strip-components 1 \
    && ./configure \
    && make \
    && make install \
    && rm -rf /usr/src/pngquant

# Install gifsicle
WORKDIR /usr/src/gifsicle

RUN curl -sSL "${GIFSICLE_URL}" | tar -xz -C /usr/src/gifsicle --strip-components 1 \
    && autoreconf -i \
    && ./configure \
    && make \
    && make install \
    && rm -rf /usr/src/gifsicle

WORKDIR /app

# Install persistent deps
RUN apk add --no-cache --virtual .persistent-deps \
    libjpeg-turbo=1.5.3-r4 \
    libpng=1.6.34-r1

# Install persistant library dependencies
# hadolint ignore=SC2046,DL3018
RUN apk add --no-cache --virtual .persistent-lib-deps \
    $( \
        scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
        | tr ',' '\n' \
        | sort -u \
        | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
    )

# Remove build dependencies
RUN apk del --purge .phpize-build-deps .build-deps

SHELL ["/bin/sh", "-c"]
