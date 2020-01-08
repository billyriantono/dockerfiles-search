FROM php:7.2-fpm-stretch

COPY conf/www.conf /usr/local/etc/php-fpm.d/www.conf

RUN ( \
apt-get update \
&& apt-get install -y --no-install-recommends \
            wget \
            libc-client-dev \
            libpq-dev \
            curl \
            libcurl3 \
            libcurl3-dev \
            libicu-dev \
            #imap-dev \
            libkrb5-dev \
            libpng-dev \
            #freetype-dev \
            libjpeg62-turbo-dev \
            libpng-dev \
            libxpm-dev \
            libvpx-dev \
            exim4 \
            gettext \
            #gettext-dev \
            #zlib-dev \
            locales \
            locales-all \
            libxml2-dev \
            libmemcached-dev \
) && ( \
 docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
 ) && ( \
 docker-php-ext-configure imap --with-imap-ssl --with-kerberos \
 ) &&( \
 docker-php-ext-configure gd \
		#--with-freetype-dir=/usr/lib/x86_64-linux-gnu/ \
		--with-jpeg-dir=/usr/lib/x86_64-linux-gnu/ \
		--with-xpm-dir=/usr/lib/x86_64-linux-gnu/ \
		#--with-vpx-dir=/usr/lib/x86_64-linux-gnu/ \
		) && ( \
 docker-php-ext-install \
        mysqli \
        pdo \
        pdo_pgsql \
        pdo_mysql \
        pgsql \
        intl \
        exif \
        pcntl \
        gettext \
        imap \
        ftp \
        gd \
        json \
        curl \
        iconv \
        mbstring \
        calendar \
        zip \
        xml \
        bcmath  \
        ) && ( \
 echo "sendmail_path=sendmail -i -t" >> /usr/local/etc/php/conf.d/php-sendmail.ini \
 ) && ( \
 wget -O - https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
) && ( \
rm -rf /var/lib/apt/lists/* \
)

RUN set -x \
    && apt-get update && apt-get install -y --no-install-recommends unzip libssl-dev libpcre3 libpcre3-dev \
    && cd /tmp \
    && curl -sSL -o php7.zip https://github.com/websupport-sk/pecl-memcache/archive/php7.zip \
    && unzip php7 \
    && cd pecl-memcache-php7 \
    && /usr/local/bin/phpize \
    && ./configure --with-php-config=/usr/local/bin/php-config \
    && make \
    && make install \
    && echo "extension=memcache.so" > /usr/local/etc/php/conf.d/ext-memcache.ini \
    && rm -rf /tmp/pecl-memcache-php7 php7.zip

RUN curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
    && mkdir -p /usr/src/php/ext/memcached \
    && tar -C /usr/src/php/ext/memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
    && docker-php-ext-configure memcached \
    && docker-php-ext-install memcached \
    && rm /tmp/memcached.tar.gz

RUN apt-get update && apt-get install -y \
        libmagickwand-dev --no-install-recommends

RUN pecl install imagick && docker-php-ext-enable imagick

COPY entrypoint.sh /usr/local/bin/
RUN chmod 777 /usr/local/bin/entrypoint.sh
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
