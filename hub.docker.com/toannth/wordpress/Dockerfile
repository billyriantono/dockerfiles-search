FROM debian:jessie

ENV WORDPRESS_VERSION 4.7.4
ENV WORDPRESS_SHA1 153592ccbb838cafa1220de9174ec965df2e9e1a  

ENV PHP_INI_DIR /usr/local/etc/php
ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data

# Apply stack smash protection to functions using local buffers and alloca()
# Make PHP's main executable position-independent (improves ASLR security mechanism, and has no performance impact on x86_64)
# Enable optimization (-O2)
# Enable linker optimization (this sorts the hash buckets to improve cache locality, and is non-default)
# Adds GNU HASH segments to generated executables (this is used if present, and is much faster than sysv hash; in this configuration, sysv hash is also generated)
# https://github.com/docker-library/php/issues/272
ENV PHP_CFLAGS="-fstack-protector-strong -fpic -fpie -O2"
ENV PHP_CPPFLAGS="$PHP_CFLAGS"
ENV PHP_LDFLAGS="-Wl,-O1 -Wl,--hash-style=both -pie"

ENV PHP_VERSION 7.1.2
ENV PHP_URL="https://secure.php.net/get/php-7.1.2.tar.xz/from/this/mirror"
ENV PHP_SHA256="d815a0c39fd57bab1434a77ff0610fb507c22f790c66cd6f26e27030c4b3e971"

ENV PHP_REDIS_VERSION 3.1.1

# persistent / runtime deps
ENV PHPIZE_DEPS \
		autoconf \
		file \
		g++ \
		gcc \
		libc-dev \
		make \
		pkg-config \
		re2c

VOLUME /var/www/html

RUN set -xe \
  \
  && buildDeps=" \
      libcurl4-openssl-dev \
      libedit-dev \
      libsqlite3-dev \
      libssl-dev \
      libxml2-dev \
      libjpeg-dev \
  		libpng12-dev \
     " \
  && fetchDeps=" \
      wget \
     " \
  && apt-get update \
  && apt-get install --no-install-recommends --no-install-suggests -y \
    $PHPIZE_DEPS \
    ca-certificates \
    curl \
    libedit2 \
    libsqlite3-0 \
    libxml2 \
    libjpeg62 \
    libpng12-0 \
    xz-utils \
    ${buildDeps} \
    ${fetchDeps} \
  && rm -r /var/lib/apt/lists/* \
  && mkdir -p $PHP_INI_DIR/conf.d \
  && mkdir -p /usr/src/php \
  && cd /usr/src \
  \
  && wget -O php.tar.xz "$PHP_URL" \
  && echo "$PHP_SHA256 *php.tar.xz" | sha256sum -c - \
  && tar -Jxf php.tar.xz -C /usr/src/php --strip-components=1 \
  \
  && export CFLAGS="$PHP_CFLAGS" \
    CPPFLAGS="$PHP_CPPFLAGS" \
    LDFLAGS="$PHP_LDFLAGS" \
  && cd /usr/src/php \
  && ./configure \
    --with-config-file-path="$PHP_INI_DIR" \
    --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
  \
    --without-pear \
  \
    --disable-cgi \
  \
  # --enable-ftp is included here because ftp_ssl_connect() needs ftp to be compiled statically (see https://github.com/docker-library/php/issues/236)
    --enable-ftp \
  # --enable-mbstring is included here because otherwise there's no way to get pecl to use it properly (see https://github.com/docker-library/php/issues/195)
    --enable-mbstring \
  # --enable-mysqlnd is included here because it's harder to compile after the fact than extensions are (since it's a plugin for several extensions, not an extension in itself)
    --enable-mysqlnd \
  \
    --with-curl \
    --with-libedit \
    --with-openssl \
    --with-zlib \
    --with-mysqli \
    --enable-opcache \
    --with-gd --with-png-dir=/usr --with-jpeg-dir=/usr \
  \
    $PHP_EXTRA_CONFIGURE_ARGS \
  && make -j "$(nproc)" \
  && make install \
  && { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; } \
  \
  # install the PHP extensions we need
  && mkdir -p /usr/src/php/ext/redis \
  && wget -O phpredis.tar.gz https://github.com/phpredis/phpredis/archive/$PHP_REDIS_VERSION.tar.gz \
  && tar -xzf phpredis.tar.gz -C /usr/src/php/ext/redis --strip-components=1 \
  && cd /usr/src/php/ext/redis \
  && phpize \
  && ./configure \
  && make \
  && make install \
  && echo "extension=redis.so" >> "/usr/local/etc/php/conf.d/redis.ini" \
  \
  && wget -O wordpress.tar.gz "https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz" \
  &&  echo "$WORDPRESS_SHA1 *wordpress.tar.gz" | sha1sum -c - \
  # upstream tarballs include ./wordpress/ so this gives us /usr/src/wordpress
  && tar -xzf wordpress.tar.gz -C /usr/src \
  && rm wordpress.tar.gz \
  && chown -R www-data:www-data /usr/src/wordpress \
  \
  && apt-get purge -y --auto-remove \
    $buildDeps \
    $fetchDeps \
    $PHPIZE_DEPS \
  && rm -rf /usr/src/php

WORKDIR /var/www/html


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

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

COPY docker-entrypoint.sh /usr/local/bin/

EXPOSE 9000

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["php-fpm"]
