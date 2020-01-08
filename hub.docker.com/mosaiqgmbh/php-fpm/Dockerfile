FROM php:7.0-fpm

LABEL maintainer=marcel.reuss@mosaiq.com \
      vendor=MOSAIQ

ENV TERM="xterm" \
    LANG="C.UTF-8" \
    LC_ALL="C.UTF-8" \
    USERID=1000 \
    GROUPID=1000

RUN useradd -ms /bin/bash mosaiq \
    && usermod -u $USERID mosaiq \
    && groupmod -g $GROUPID mosaiq \
    && usermod -a -G root mosaiq \
    && mkdir -p /opt/run \
    && chown mosaiq -R /opt/run \
    && chgrp mosaiq -R /opt/run

COPY conf/ /opt/docker/

RUN set -x \
    && apt-get update \
    && RUNLEVEL=1 apt-get dist-upgrade -y -f \
    && apt-get install -y -f --no-install-recommends \
        apt-transport-https \
        ca-certificates \
        locales \
        gnupg

RUN set -x \
    && apt-get install -y -f --no-install-recommends \
        supervisor \
        wget \
        curl \
        vim \
        cron \
        net-tools \
        tzdata

RUN set -x \
    && apt-get install -y -f --no-install-recommends \
        zip \
        unzip \
        bzip2 \
        moreutils \
        dnsutils \
        openssh-client \
        mysql-client \
        rsync \
        git \
        patch \
        locales-all

RUN set -x \
    && apt-get install -y -f --no-install-recommends \
        imagemagick \
        graphicsmagick \
        ghostscript \
        jpegoptim \
        libjpeg-turbo-progs \
        pngcrush \
        optipng \
        apngopt \
        pngnq \
        pngquant \
        libldap-2.4-2 \
        libxslt1.1 \
        zlibc \
        zlib1g \
        libpq5 \
        libpng16-16 \
        libmcrypt4 \
        libzip4 \
        libjpeg62-turbo-dev \
        libfreetype6-dev \
        libbz2-dev \
        libicu-dev \
        libldap2-dev \
        libldb-dev \
        libmcrypt-dev \
        libxml2-dev \
        libxslt1-dev \
        zlib1g-dev \
        libmemcached-dev \
        libpng-dev \
        libpq-dev \
        libzip-dev \
        libc-client-dev \
        libkrb5-dev \
    && wget https://github.com/google/guetzli/archive/master.zip \
    && unzip master.zip \
    && make -C guetzli-master \
    && cp guetzli-master/bin/Release/guetzli /usr/local/bin/ \
    && rm -rf master.zip guetzli-master \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install \
        bcmath \
        bz2 \
        calendar \
        exif \
        intl \
        imap \
        gettext \
        ldap \
        mysqli \
        mcrypt \
        hash \
        pcntl \
        pdo_mysql \
        pdo_pgsql \
        pgsql \
        soap \
        sockets \
        tokenizer \
        sysvmsg \
        sysvsem \
        sysvshm \
        shmop \
        xmlrpc \
        xsl \
        zip \
        gd \
        gettext \
        opcache \
    && pecl install apcu \
    && printf "no --disable-memcached-sasl\n" | pecl install memcached-3.0.4 \
    && echo extension=memcached.so > /usr/local/etc/php/conf.d/memcached.ini \
    && pecl install redis \
    && pecl install mongodb \
    && echo extension=apcu.so > /usr/local/etc/php/conf.d/apcu.ini \
    && echo extension=redis.so > /usr/local/etc/php/conf.d/redis.ini \
    && echo extension=mongodb.so > /usr/local/etc/php/conf.d/mongodb.ini \
    && apt-get purge -y -f --force-yes \
        libc-client-dev \
        libkrb5-dev \
        libbz2-dev \
        libicu-dev \
        libldap2-dev \
        libldb-dev \
        libmcrypt-dev \
        libxml2-dev \
        libxslt1-dev \
        zlib1g-dev \
        libpng-dev \
        libpq-dev \
        libzip-dev \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y nodejs \
    && apt-get autoremove -y -f \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

RUN set -x \
    && ln -sf "/opt/docker/etc/php/php.custom.ini" "/usr/local/etc/php/conf.d/99-docker.ini" \
    && crontab /opt/docker/etc/cron/crontab

EXPOSE 9000
CMD ["supervisord", "-c", "/opt/docker/etc/supervisor.conf", "--logfile", "/dev/null", "--pidfile", "/dev/null", "--user", "mosaiq"]
