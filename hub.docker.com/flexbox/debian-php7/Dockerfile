FROM php:fpm

LABEL maintainer="Alex Karshin <https://flexbox.it>"
LABEL source="https://bitbucket.org/flexboxIT/debian-php7"

RUN usermod -u 1000 www-data
RUN groupmod -g 1000 www-data

RUN apt-get update \
    && apt-get install -y \
        apt-utils \
        aspell-cs \
        aspell-en \
        aspell-ru \
        build-essential \
        curl \
	    libc-client-dev \
        libcurl3 \
        libcurl3-dev \
        libfreetype6-dev \
        libicu-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        mysql-client \
        libkrb5-dev \
        libpng12-dev \
        libpq-dev \
        libpspell-dev \
        libssl-dev \
        libxml2-dev \
        libxslt-dev \
        php-apc \
    && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-install -j$(nproc) bcmath \
    && docker-php-ext-install -j$(nproc) calendar \
    && docker-php-ext-install -j$(nproc) ctype \
    && docker-php-ext-install -j$(nproc) dom \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) hash \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install -j$(nproc) imap \
    && docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-install -j$(nproc) json \
    && docker-php-ext-install -j$(nproc) mbstring \
    && docker-php-ext-install -j$(nproc) mcrypt \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) pdo \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) pdo_pgsql \
    && docker-php-ext-install -j$(nproc) pspell \
    && docker-php-ext-install -j$(nproc) session \
    && docker-php-ext-install -j$(nproc) sockets \
    && docker-php-ext-install -j$(nproc) tokenizer \
    && docker-php-ext-install -j$(nproc) xml \
    && docker-php-ext-install -j$(nproc) xmlrpc \
    && docker-php-ext-install -j$(nproc) xmlwriter \
    && docker-php-ext-install -j$(nproc) zip \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y nginx

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

COPY start.sh /tmp/start.sh
COPY php.ini /usr/local/etc/php/conf.d/memory.ini

WORKDIR /html

EXPOSE 80 443

CMD ["/tmp/start.sh"]
