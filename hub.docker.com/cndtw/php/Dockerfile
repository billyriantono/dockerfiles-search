FROM php:7.1.20-fpm

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /tmp/composer
ENV COMPOSER_VERSION 1.6.5
ENV TINI_VERSION v0.17.0

ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

ENTRYPOINT ["/tini", "-s", "--", "docker-php-entrypoint"]

RUN set -x && \
    apt-get update && \
    apt-get -y upgrade libgcrypt20 perl && \
    apt-get -y install --no-install-recommends apt-transport-https apt-utils gnupg2 && \
    curl -s https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl -s https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
    apt-get update && \
    ACCEPT_EULA=Y apt-get -y install --no-install-recommends \
    libmcrypt-dev \
    zlib1g-dev \
    unzip \
    git \
    libpng++-dev \
    libwebp-dev \
    libxml2-dev \
    libxslt-dev \
    libsqlite3-dev \
    unixodbc-dev \
    msodbcsql \
    libfcgi-bin \
    libmagickwand-dev && \
    docker-php-ext-configure gd --with-jpeg-dir=/usr --with-png-dir=/usr && \
    docker-php-ext-install -j$(nproc) \
    bcmath calendar exif mcrypt \
    pdo_mysql pdo_sqlite \
    shmop wddx xsl \
    zip \
    opcache \
    gd && \
    curl -s https://getcomposer.org/installer | php -- --install-dir=/bin --filename=composer --version=${COMPOSER_VERSION} && \
    pecl install sqlsrv && \
    pecl install pdo_sqlsrv && \
    pecl install imagick && \
    docker-php-ext-enable pdo_sqlsrv sqlsrv imagick && \
    rm -rf /var/lib/apt/lists/* /tmp/*

CMD ["php-fpm"]
