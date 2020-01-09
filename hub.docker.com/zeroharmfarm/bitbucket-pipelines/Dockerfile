FROM ubuntu:yakkety

RUN apt-get update && apt-get dist-upgrade -y
RUN apt-get install -y \
        curl \
        git \
        php7.0-cli \
        php7.0-json \
        php7.0-mysql \
        php7.0-sqlite3 \
        php7.0-mbstring \
        php7.0-gd \
        php7.0-intl \
        php7.0-memcached \
        php7.0-xml \
        php7.0-zip \
    && curl -sL https://deb.nodesource.com/setup_7.x | bash - \
    && apt-get install -y nodejs \
    && apt-get -y autoremove && apt-get clean

RUN curl -sSL https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/bin

# This Dockerfile doesn't need to have an entrypoint and a command
# as Bitbucket Pipelines will overwrite it with a bash script.