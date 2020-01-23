FROM php:fpm-alpine as base
RUN apk update

FROM base
RUN apk --no-cache add \
    git \
    libzip \
    libzip-dev \
    libxml2 \
    libxml2-dev \
    libcurl \
    curl-dev \
    bash

#Configure and install GD

RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev && \
  docker-php-ext-configure gd \
    --with-gd \
    --with-freetype-dir=/usr/include/ \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ && \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
  docker-php-ext-install -j${NPROC} gd

#Install deps for PHP

RUN docker-php-ext-install zip xml exif opcache simplexml session mbstring json dom ctype curl && \
    apk del --no-cache libzip-dev libxml2-dev curl-dev freetype-dev libpng-dev libjpeg-turbo-dev

#adding local user

ENV UID=1000
ENV GID=1000
ENV USER=wapssy
ENV WEBDIR=webdir
RUN addgroup --gid "$GID" "$USER" \
    && adduser \
    --disabled-password \
    --shell bin/bash \
    --gecos "" \
    --home "$(pwd)" \
    --ingroup "$USER" \
    --no-create-home \
    --uid "$UID" \
    "$USER"
    
# installing composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Create directories for scripts
RUN mkdir /scripts && \
    chown 1000:1000 /scripts -R
COPY ./scripts/install.sh /scripts/install.sh

# change user and work dir.
USER wapssy
WORKDIR /web/html
