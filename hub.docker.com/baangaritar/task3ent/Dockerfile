FROM phusion/baseimage

ENV HOME /root


RUN (usermod -u 1000 www-data)
RUN (groupmod -g 1000 www-data)
RUN (usermod -d /home/www-data www-data)
RUN mkdir -p /home/www-data/.ssh
RUN chown -R 1000:1000 /home/www-data
#may not need to change file perms
#RUN (find / -uid 1000 -exec chown -h 5000 '{}' \+)

# persistent / runtime deps
RUN apt-get update
RUN apt-get install -y \
    ca-certificates \
	curl \
    libcurl3 \
	librecode0 \
	libsqlite3-0 \
	libpng12-dev \
	libxml2 \
	zip \
	unzip \
	libjpeg-dev \
	autoconf \
	file \
	g++ \
	gcc \
	libc-dev \
	make \
	pkg-config \
	re2c \
	wget \
	nano \
    ssh \
    npm \
	python-software-properties \
	build-essential \
	pkg-config \
	libmcrypt-dev \
    libyaml-dev \
    libssl-dev \
    libsslcommon2-dev \
    libcurl4-openssl-dev \
    libxml2-dev \
    xz-utils \
    libxslt1.1 \
    libxslt1-dev \
    libicu-dev \
    libicu55 \
    libmcrypt4  \
    libjpeg-dev \
    libpng12-dev \
    libsqlite3-0 \
    libxml2 \
    zip \
    git \
    unzip \
    libxslt1.1 \
	libgpgme11-dev \
    ssmtp \
	--no-install-recommends
#RUN apt-get install -y rsyslog syslog-ng

RUN ln -s /usr/bin/nodejs /usr/bin/node \
  && npm install -g n \
  && n lts

RUN echo "deb http://nginx.org/packages/ubuntu/ trusty nginx " > /etc/apt/sources.list.d/nginx.list
RUN echo "deb-src http://nginx.org/packages/ubuntu/ trusty nginx" >> /etc/apt/sources.list.d/nginx.list

RUN wget http://nginx.org/keys/nginx_signing.key
RUN apt-key add nginx_signing.key

#nginx
RUN apt-get update
RUN apt-get install -y --force-yes nginx
RUN rm -r /var/lib/apt/lists/*

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN echo "error_log /dev/stdout info;" >> /etc/nginx/nginx.conf

###################php 7

ENV PHP_INI_DIR /usr/local/etc/php
RUN mkdir -p $PHP_INI_DIR/conf.d

# Apply stack smash protection to functions using local buffers and alloca()
# Make PHP's main executable position-independent (improves ASLR security mechanism, and has no performance impact on x86_64)
# Enable optimization (-O2)
# Enable linker optimization (this sorts the hash buckets to improve cache locality, and is non-default)
# Adds GNU HASH segments to generated executables (this is used if present, and is much faster than sysv hash; in this configuration, sysv hash is also generated)
# https://github.com/docker-library/php/issues/272
ENV CFLAGS="-fstack-protector-strong -fpic -fpie -O2"
ENV CPPFLAGS="$CFLAGS"
ENV LDFLAGS="-Wl,-O1 -Wl,--hash-style=both"

ENV GPG_KEYS A917B1ECDA84AEC2B568FED6F50ABC807BD5DCD0 528995BFEDFBA7191D46839EF9BA0ADA31CBD89E

ENV PHP_VERSION 7.1.10
ENV PHP_URL="https://secure.php.net/get/php-7.1.10.tar.xz/from/this/mirror"
ENV PHP_ASC_URL="https://secure.php.net/get/php-7.1.10.tar.xz.asc/from/this/mirror"
ENV PHP_SHA256="2b8efa771a2ead0bb3ae67b530ca505b5b286adc873cca9ce97a6e1d6815c50b"
ENV PHP_MD5=""

RUN set -xe; \
    \
    fetchDeps=' \
        wget \
    '; \
    apt-get update; \
    apt-get install -y --no-install-recommends $fetchDeps; \
    rm -rf /var/lib/apt/lists/*; \
    \
    mkdir -p /usr/src; \
    cd /usr/src; \
    \
    wget -O php.tar.xz "$PHP_URL"; \
    \
    if [ -n "$PHP_SHA256" ]; then \
        echo "$PHP_SHA256 *php.tar.xz" | sha256sum -c -; \
    fi; \
    if [ -n "$PHP_MD5" ]; then \
        echo "$PHP_MD5 *php.tar.xz" | md5sum -c -; \
    fi; \
    \
    if [ -n "$PHP_ASC_URL" ]; then \
        wget -O php.tar.xz.asc "$PHP_ASC_URL"; \
        export GNUPGHOME="$(mktemp -d)"; \
        for key in $GPG_KEYS; do \
            gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
        done; \
        gpg --batch --verify php.tar.xz.asc php.tar.xz; \
        rm -r "$GNUPGHOME"; \
    fi; \
    \
    apt-get purge -y --auto-remove $fetchDeps

COPY Dockerbuild/docker-php-source /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-php-source

ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data
RUN set -xe \
    && buildDeps=" \
        $PHP_EXTRA_BUILD_DEPS \
        libcurl4-openssl-dev \
        libreadline6-dev \
        librecode-dev \
        libsqlite3-dev \
        libssl-dev \
        libxml2-dev \
        libfreetype6-dev \
        xz-utils \
    " \
    && apt-get update && apt-get install -y $buildDeps --no-install-recommends && rm -rf /var/lib/apt/lists/* \
    \
    && docker-php-source extract \
    && cd /usr/src/php \
    && ./configure \
        --with-config-file-path="$PHP_INI_DIR" \
        --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
        \
        --disable-cgi \
        \
# --enable-ftp is included here because ftp_ssl_connect() needs ftp to be compiled statically (see https://github.com/docker-library/php/issues/236)
        --enable-ftp \
        --enable-mysqlnd \
        --with-mysqli \
        --with-curl \
        --with-openssl \
        --with-readline \
        --with-recode \
        --with-zlib \
        --with-gd \
        --enable-xdebug \
        --with-jpeg-dir=/usr/lib/x86_64-linux-gnu \
        --with-pdo-mysql \
        --enable-mbstring \
        --with-mcrypt \
        --enable-soap \
        --enable-intl \
        --enable-bcmath \
        --enable-simplexml \
        --with-mhash \
        --with-xsl \
        --enable-zip \
        --enable-caneldar \
        --with-freetype-dir=/usr/include/freetype2 \
        --enable-gd-native-ttf \
        $PHP_EXTRA_CONFIGURE_ARGS \
    && make -j "$(nproc)" \
    && make install \
    && { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; } \
    && make clean \
    && docker-php-source delete
#apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps

    WORKDIR /var/www

    RUN set -ex \
        && cd /usr/local/etc \
        && if [ -d php-fpm.d ]; then \
            # for some reason, upstream's php-fpm.conf.default has "include=NONE/etc/php-fpm.d/*.conf"
            sed 's!=NONE/!=!g' php-fpm.conf.default | tee php-fpm.conf > /dev/null; \
            cp php-fpm.d/www.conf.default php-fpm.d/www.conf; \
        else \
            # PHP 5.x doesn't use "include=" by default, so we'll create our own simple config that mimics PHP 7+ for consistency
            mkdir php-fpm.d; \
            cp php-fpm.conf.default php-fpm.d/www.conf; \
            { \
                echo '[global]'; \
                echo 'include=etc/php-fpm.d/*.conf'; \
            } | tee php-fpm.conf; \
        fi \
        && { \
            echo '[global]'; \
            echo 'error_log = /proc/self/fd/2'; \
            echo; \
            echo '[www]'; \
            echo '; if we send this to /proc/self/fd/1, it never appears'; \
            echo 'access.log = /proc/self/fd/2'; \
            echo; \
            echo 'clear_env = no'; \
            echo; \
            echo '; Ensure worker stdout and stderr are sent to the main error log.'; \
            echo 'catch_workers_output = yes'; \
        } | tee php-fpm.d/docker.conf \
        && { \
            echo '[global]'; \
            echo 'daemonize = no'; \
            echo; \
            echo '[www]'; \
            echo 'listen = [::]:9000'; \
        } | tee php-fpm.d/zz-docker.conf

####Install PECL modules
RUN pecl install gnupg
RUN pecl install mongodb
RUN pecl install yaml
####END PHP


#Install xdebug
#RUN apt-get update
#RUN apt-get install -y git-core
#RUN git clone https://github.com/xdebug/xdebug.git /tmp/xdebug
#RUN cd /tmp/xdebug && phpize && ./configure --enable-xdebug && make
#RUN mkdir /usr/local/etc/php/modules
#RUN cp /tmp/xdebug/modules/xdebug.so /usr/local/etc/php/modules/xdebug.so
#RUN cd / && rm -rf /tmp/xdebug

#Install EBcli
#RUN apt-get install -y ruby
#RUN curl -O https://bootstrap.pypa.io/get-pip.py && python2.7 get-pip.py
#RUN pip install awsebcli


RUN mkdir -p /var/www &&\
    chown -R www-data:www-data /var/www &&\
    chmod -R 777 /var/www

RUN mkdir                       /etc/service/nginx
RUN mkdir                       /etc/service/phpfpm
RUN mkdir                       /root/.composer
ADD Dockerbuild/nginx.conf      /buildfiles/nginx.conf
ADD Dockerbuild/ssmtp.conf   	/etc/ssmtp/ssmtp.conf
#RUN mkdir                       /root/.ssh
ADD Dockerbuild/default         /etc/nginx/conf.d/default.conf
ADD Dockerbuild/nginx.sh        /etc/service/nginx/run
ADD Dockerbuild/phpfpm.sh       /etc/service/phpfpm/run
ADD Dockerbuild/auth.json       /root/.composer/auth.json
#ADD Dockerbuild/graylog.conf   /etc/rsyslog.d/graylog.conf
ADD Dockerbuild/php.ini         /usr/local/etc/php/php.ini

RUN chmod +x                    /etc/service/nginx/run
RUN chmod +x                    /etc/service/phpfpm/run

#CMD service rsyslog start && /sbin/my_init

COPY Dockerbuild/init.sh /sbin/init
RUN chmod +x /sbin/init
CMD ["/sbin/init"]
