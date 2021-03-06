FROM ubuntu:16.04

# persistent / runtime deps
ENV PHPIZE_DEPS \
		autoconf \
		dpkg-dev \
		file \
		g++ \
		gcc \
		libpcre3-dev \
		make \
		pkg-config \
		re2c
RUN apt-get update && apt-get install -y \
		$PHPIZE_DEPS \
		ca-certificates \
		curl \
		libedit2 \
		libsqlite3-0 \
		libxml2 \
		xz-utils \
	&& rm -r /var/lib/apt/lists/*

ENV PHP_INI_DIR /usr/local/etc/php
RUN mkdir -p $PHP_INI_DIR/conf.d

##<autogenerated>##
ENV PHP_EXTRA_CONFIGURE_ARGS --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data
##</autogenerated>##

# Apply stack smash protection to functions using local buffers and alloca()
# Make PHP's main executable position-independent (improves ASLR security mechanism, and has no performance impact on x86_64)
# Enable optimization (-O2)
# Enable linker optimization (this sorts the hash buckets to improve cache locality, and is non-default)
# Adds GNU HASH segments to generated executables (this is used if present, and is much faster than sysv hash; in this configuration, sysv hash is also generated)
# https://github.com/docker-library/php/issues/272
ENV PHP_CFLAGS="-fstack-protector-strong -fpic -fpie -O2"
ENV PHP_CPPFLAGS="$PHP_CFLAGS"
ENV PHP_LDFLAGS=""

ENV GPG_KEYS A917B1ECDA84AEC2B568FED6F50ABC807BD5DCD0 528995BFEDFBA7191D46839EF9BA0ADA31CBD89E

ENV PHP_VERSION 7.1.5
ENV PHP_URL="https://secure.php.net/get/php-7.1.5.tar.xz/from/this/mirror" PHP_ASC_URL="https://secure.php.net/get/php-7.1.5.tar.xz.asc/from/this/mirror"
ENV PHP_SHA256="d149a3c396c45611f5dc6bf14be190f464897145a76a8e5851cf18ff7094f6ac" PHP_MD5="fb0702321c7aceac68c82b8c7a10d196"

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
	fi;

COPY docker-php-source /usr/local/bin/

RUN set -xe \
	&& buildDeps=" \
		$PHP_EXTRA_BUILD_DEPS \
		libcurl4-openssl-dev \
		libedit-dev \
		libsqlite3-dev \
		libssl-dev \
		libxml2-dev \
		libkrb5-dev \
		libpam0g \
		libpam0g-dev \
		mlock \
		libc-client-dev \
		libkrb5-dev \
		sudo \
		libcurl4-openssl-dev \
		curl \
		python-pip \
		apt-transport-https \
		apt-utils \
		libmcrypt-dev \
		zip \
		unzip \
		postgresql-server-dev-all \
		libfreetype6-dev tzdata \
		libturbojpeg \
		libpng12-dev \
		supervisor \
		cron \
		locales \
		libjpeg-turbo8-dev \
	" \
	&& apt-get update && apt-get install -y $buildDeps && rm -r /var/lib/apt/lists/*

RUN export CFLAGS="$PHP_CFLAGS" \
		CPPFLAGS="$PHP_CPPFLAGS" \
		LDFLAGS="$PHP_LDFLAGS" \
	&& docker-php-source extract \
	&& cd /usr/src/php \
	&& gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	&& ./configure \
		--build="$gnuArch" \
		--with-config-file-path="$PHP_INI_DIR" \
		--with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
		\
		--disable-cgi \
		\
		--enable-ftp \
		--enable-mbstring \
		--enable-mysqlnd \
		\
		--with-curl \
		--with-libedit \
		--with-openssl \
		--with-zlib \
		--with-pcre-regex=/usr \
		--with-libdir="lib/$gnuArch" \
		\
		$PHP_EXTRA_CONFIGURE_ARGS \
	&& make -j "$(nproc)" \
	&& make install \
	&& { find /usr/local/bin /usr/local/sbin -type f -executable -exec strip --strip-all '{}' + || true; } \
	&& make clean \
	&& docker-php-source delete

COPY docker-php-ext-* docker-php-entrypoint /usr/local/bin/

ENTRYPOINT ["docker-php-entrypoint"]
##<autogenerated>##
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

EXPOSE 9000

RUN echo "Europe/Moscow" > /etc/timezone && \
        dpkg-reconfigure -f noninteractive tzdata && \
        sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
        sed -i -e 's/# ru_RU.UTF-8 UTF-8/ru_RU.UTF-8 UTF-8/' /etc/locale.gen && \
        echo 'LANG="ru_RU.UTF-8"'>/etc/default/locale && \
        dpkg-reconfigure --frontend=noninteractive locales && \
        update-locale LANG=ru_RU.UTF-8
        
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
RUN docker-php-ext-configure imap --with-imap --with-imap-ssl --with-kerberos

RUN docker-php-ext-install \
	curl \
	iconv \
	mcrypt \
	calendar \
	imap \
	mbstring \
	pdo_mysql \
	tokenizer \
	pdo_pgsql \
	gd \
	exif \
	bcmath \
	opcache \
	sockets \
	zip

RUN usermod  -u 1000 www-data
RUN groupmod -g 1000 www-data

COPY .crontab /etc/cron.d/composer
COPY schedule.sh /root/schedule.sh
COPY job.sh /root/job.sh
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN chmod 744 /root/schedule.sh && \
	chmod 744 /root/job.sh && \
	chmod 644 /etc/cron.d/composer && \
	rm /etc/localtime && \
	ln -s /usr/share/zoneinfo/Europe/Moscow /etc/localtime && \
	echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini && \
	echo "upload_max_filesize=100M" > $PHP_INI_DIR/conf.d/upload_max_filesize.ini && \
	echo "post_max_size=100M" > $PHP_INI_DIR/conf.d/post_max_size.ini && \
	echo "max_input_vars=100000" > $PHP_INI_DIR/conf.d/max_input_vars.ini && \
	echo "max_input_time=300" > $PHP_INI_DIR/conf.d/max_input_time.ini

RUN cd / && \
    apt-get update && \
    apt-get install -y git && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    php composer.phar create-project composer/satis --stability=dev

COPY .ssh /var/www/.ssh
RUN ssh-keyscan -t rsa -H gitlab.sorokarm.ru >> /var/www/.ssh/known_hosts && \
    chown -R www-data:www-data /var/www

CMD ["/usr/bin/supervisord"]
