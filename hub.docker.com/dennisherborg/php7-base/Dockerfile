FROM alpine:latest

RUN apk --update add \
    bash \
    sudo \

    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    bzip2 \
    libbz2 \
    libxml2-dev \
    libxslt-dev \
    openssl \
    openssh-client \

    php7 \
    php7-iconv \
    php7-mcrypt \
    php7-gd \
    php7-bz2 \
    php7-calendar \
    php7-exif \
    php7-ftp \
    php7-gettext \
    php7-mysqli \
    php7-pdo_mysql \
    php7-sockets \
    php7-wddx \
    php7-xsl \
    php7-zip \
    php7-openssl \
    php7-json \
    php7-phar \
    php7-zlib \
    php7-mbstring \
    php7-xml \
    php7-xmlreader \
    php7-bcmath \
    php7-pcntl \
    php7-pear \
    php7-ctype \
    php7-opcache \
    php7-soap \
    php7-intl \
    php7-ftp \
    php7-session \
    php7-posix \
    php7-curl \
    php7-xmlwriter \
    php7-tokenizer \
    php7-simplexml \
    php7-imap \

    libssl1.0 \
    curl \
    wget && \

    apk del build-base && \
    rm -f /var/cache/apk/* && \

    echo "date.timezone=Europe/Berlin" > /etc/php7/conf.d/timezone.ini

ENV GOSU_VERSION 1.10
ENV DOCKERIZE_VERSION v0.6.0

# Install Gosu
RUN set -x \
    && apk add --no-cache --virtual .gosu-deps \
        dpkg \
        gnupg \
    && dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')" \
    && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch" \
    && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch.asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && GPG_KEY="B42F6819007F00F88E364FD4036A9C25BF357DD4" \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$GPG_KEY" || gpg --keyserver pgp.mit.edu --recv-keys "$GPG_KEY" || gpg --keyserver keyserver.pgp.com --recv-keys "$GPG_KEY" \
    && gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
    && rm -rf "$GNUPGHOME" /usr/local/bin/gosu.asc \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true \
    && apk del .gosu-deps &&\

# Install dockerize
    mkdir -p /usr/local/bin/ &&\
    curl -SL https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz \
    | tar xzC /usr/local/bin &&\
    rm -rf /var/cache/apk/* /tmp/* /var/tmp/*

WORKDIR /app

CMD []
