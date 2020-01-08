FROM wordpress:php7.0-fpm

LABEL version="1.0"
LABEL description="TPT's WP CircleCI container."
LABEL maintainer="phughes@playerstribune.com"

# ######################################################################
# Install apt system packages
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends \
    ssh-client   \
    git          \
    subversion   \
    mysql-server

# ######################################################################
# Install Composer
# Update this to change Composer install version. This is 1.5.2 (2017-09-11).
ENV COMPOSER_COMMIT_HASH="4449596339f6ee0b9bbe21117eb7998fd46fbd25"
ENV COMPOSER_INSTALLER_URL="https://raw.githubusercontent.com/composer/getcomposer.org/$COMPOSER_COMMIT_HASH/web/installer"
RUN curl -q "$COMPOSER_INSTALLER_URL" | php -- --quiet && \
    mv composer.phar /usr/local/bin/composer

# ######################################################################
# Install Dockerize
# Helps to avoid race conditions when spinning up next to a DB container
ENV DOCKERIZE_VERSION="v0.5.0"
ENV DOCKERIZE_INSTALLER_URL="https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz"
RUN curl -qLO "$DOCKERIZE_INSTALLER_URL" \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# ######################################################################
# Add php.ini file, to suppress warnings mostly
RUN mkdir -p /usr/src/php && \
    tar --file /usr/src/php.tar.xz --extract --strip-components=1 --directory /usr/src/php && \
    cp /usr/src/php/php.ini-development /usr/local/etc/php/php.ini
