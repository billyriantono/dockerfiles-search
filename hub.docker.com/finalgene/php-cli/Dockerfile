FROM php:7.3-cli-alpine3.10

LABEL maintainer="frank.giesecke@final-gene.de"

ARG PHPREDIS_VERSION="5.0.2"
ENV XDEBUG_VERSION="2.7.2"

# Install build dependencies
# hadolint ignore=SC2086,DL3018
RUN apk add --no-cache \
        ${PHPIZE_DEPS} \
        bash \
        gettext-dev \
        icu-dev \
        krb5-dev \
        libpng-dev \
        libxml2-dev \
        libxslt-dev \
        openldap-dev \
        postgresql-dev \
        libzip-dev \
        imap-dev

SHELL ["/bin/bash", "-o", "pipefail", "-e", "-c"]

# Provide sources to build PHP redis client
RUN mkdir -p /usr/src/php/ext/redis \
    && curl -sSL "https://github.com/phpredis/phpredis/archive/${PHPREDIS_VERSION}.tar.gz" | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts

# Configure and install PHP extensions
RUN docker-php-ext-configure \
        imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install \
        bcmath \
        calendar \
        exif \
        gd \
        gettext \
        imap \
        intl \
        ldap \
        mysqli \
        opcache \
        pcntl \
        pdo_mysql \
        pdo_pgsql \
        redis \
        shmop \
        soap \
        sockets \
        sysvmsg \
        sysvsem \
        sysvshm \
        wddx \
        xsl \
        zip

# Install XDEBUG
RUN pecl install "xdebug-${XDEBUG_VERSION}"

# Add entrypoint
COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

# Configure working directory
WORKDIR /app

# Configure entrypoint
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD [""]
