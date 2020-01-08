FROM php:7.2-fpm-stretch

RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' > /etc/timezone

RUN apt-get clean all \
    && apt-get update \
    # develop utils
    && apt-get install -y --no-install-recommends \
        git \
        net-tools \
        nmap \
        iputils-ping \
        procps \
        tofrodos \
    # php depend libs
    && apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libxml2-dev \
        libxslt-dev \
        libbz2-dev \
    && docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install xsl \
    && docker-php-ext-install bz2 \
    && docker-php-ext-install zip \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install exif \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install sockets \
    && docker-php-ext-install gettext \
    && docker-php-ext-install sysvmsg \
    && docker-php-ext-install sysvsem \
    && docker-php-ext-install sysvshm \
    && docker-php-ext-install opcache

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups

RUN cd /tmp/ \
    && git clone -b '3.1.6' https://github.com/phpredis/phpredis.git redis-3.1.6 \
    && ( cd redis-3.1.6 && phpize && ./configure && make && make install && cd ..) \
    && rm -r redis-3.1.6 \
    && docker-php-ext-enable redis

ENV PHPFPM_INI_DIR=/usr/local/etc/php-fpm.d

RUN sed -i '\
    s/user = www-data/user = root/;\
    s/group = www-data/group = root/;\
    s/pm.max_children = 5/pm.max_children = 200/g;\
    s/pm.start_servers = 2/pm.start_servers = 20/g;\
    s/pm.min_spare_servers = 1/pm.min_spare_servers = 20/g;\
    s/pm.max_spare_servers = 3/pm.max_spare_servers = 200/g;\
    ' $PHPFPM_INI_DIR/www.conf

COPY ./php.ini $PHP_INI_DIR/

ENV DBGP_URL=http://downloads.activestate.com/Komodo/releases/11.1.0/remotedebugging/Komodo-PythonRemoteDebugging-11.1.0-91033-linux-x86_64.tar.gz
RUN apt-get install -y python \
    # 配置 DBGP
    && cd /usr/src \
    && curl -o dbgp.tar.gz $DBGP_URL \
    && tar zxvf dbgp.tar.gz \
    && mv `ls -l|grep Komodo|awk '{print $9}'` /usr/local/dbgp \
    && rm -rf dbgp.tar.gz

ENV XDEBUG_VERSION=2.7.2

COPY ./docker-php-ext-xdebug.ini /tmp/

#$PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini

RUN cd /usr/src \
    && curl -O https://xdebug.org/files/xdebug-$XDEBUG_VERSION.tgz\
    && tar zxf xdebug-$XDEBUG_VERSION.tgz \
    && ( cd xdebug-$XDEBUG_VERSION && phpize && ./configure && make && make install && cd ..) \
    && rm -rf ./xdebug-* \
    && docker-php-ext-enable xdebug \
    && cat /tmp/docker-php-ext-xdebug.ini >> $PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini \
    && rm /tmp/docker-php-ext-xdebug.ini

COPY entrypoint.sh /entrypoint.sh

RUN apt-get clean \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /usr/src/*

WORKDIR /var/www/

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/usr/local/sbin/php-fpm", "-R"]

EXPOSE 9000
EXPOSE 10001