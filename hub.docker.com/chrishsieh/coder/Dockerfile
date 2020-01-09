FROM php:fpm

ENV DEBCONF_NOWARNINGS yes

# Make info file about this build
RUN set -x \
    && apt-get update \
    && apt-get install -y gnupg2 \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash -\
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apt-get update \
    && apt-get install -y \
        gettext jq figlet \
        zip git ruby-full nodejs \
        libpng-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libicu-dev locales locales-all mysql-client wget \
        libmemcachedutil2 libmemcached-dev libc6 \
        openssl net-tools sudo dumb-init \
    && apt-get install -y curl cmake \
    && mkdir /tmp/libzip && cd /tmp/libzip && curl -sSLO https://libzip.org/download/libzip-1.5.1.tar.gz \
    && tar zxf libzip-1.5.1.tar.gz && cd libzip-1.5.1/ && mkdir build && cd build && cmake ../ \
    && make > /dev/null && make install \
    && docker-php-ext-configure zip \
        --with-libzip=/usr/local/lib/libzip.so \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-install -j${NPROC} \
        intl gettext mysqli pdo_mysql exif gd zip \
    && pecl channel-update pecl.php.net \
    && pecl install xdebug-2.7.0RC2 \
    && docker-php-ext-enable xdebug \
    && (rm -rf /usr/local/lib/php/test/xdebug || true) \
    && (rm -rf /usr/local/lib/php/doc/xdebug || true) \
    && pecl install memcached \
    && docker-php-ext-enable memcached \
    && (rm -rf /usr/local/lib/php/test/memcached || true) \
    && (rm -rf /usr/local/lib/php/doc/memcached || true) \
    && apt-get purge -y \
        libpng-dev \
        libzip-dev \
        libfreetype6-dev \
        libicu-dev cmake \
        libmemcached-dev \
    && apt-get autoremove -y \
    && npm i npm@latest -g \
    && composer self-update \
    && composer global require hirak/prestissimo \
    && gem install sass -v 3.4.25

COPY ./presetup /usr/local/bin
COPY ./code-server.tar.gz /usr/local/bin
RUN cd /usr/local/bin && tar zxvf code-server.tar.gz
COPY ./php.ini /usr/local/etc/php/
RUN chmod +x /usr/local/bin/presetup

RUN locale-gen en_US.UTF-8
# We unfortunately cannot use update-locale because docker will not use the env variables
# configured in /etc/default/locale so we need to set it manually.
ENV LC_ALL=en_US.UTF-8

RUN adduser --gecos '' --disabled-password coder && \
	echo "coder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/nopasswd

USER coder
# We create first instead of just using WORKDIR as when WORKDIR creates, the user is root.
RUN mkdir -p /home/coder/project
WORKDIR /home/coder/project

EXPOSE 8443

# Run the configsetup file on container start
ENTRYPOINT ["/usr/local/bin/presetup"]
CMD ["dumb-init", "code-server"]
