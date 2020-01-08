FROM php:7.2-fpm-alpine

### next is based on: https://github.com/docker-library/wordpress/blob/master/php7.2/fpm-alpine/Dockerfile
# docker-entrypoint.sh dependencies
RUN apk add --no-cache \
# in theory, docker-entrypoint.sh is POSIX-compliant, but priority is a working, consistent image
		bash \
# BusyBox sed is not sufficient for some of our sed expressions
		sed
### end

### own code
# Use the default production configuration
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

RUN apk --update add git \
  build-base \
  libmemcached-dev \
  libmcrypt-dev \
  libxml2-dev \
  zlib-dev \
  autoconf \
  cyrus-sasl-dev \
  libgsasl-dev

RUN docker-php-ext-install mysqli mbstring pdo pdo_mysql tokenizer xml opcache zip

RUN pecl channel-update pecl.php.net
RUN pecl install mcrypt-1.0.1 && docker-php-ext-enable mcrypt

## install xdebug, make sure the ini is set
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini
### end own code

### next is based on: https://github.com/docker-library/wordpress/blob/master/php7.2/fpm-alpine/Dockerfile
# install the PHP extensions we need for WP
RUN set -ex; \
	\
	apk add --no-cache --virtual .build-deps \
		libjpeg-turbo-dev \
		libpng-dev \
	; \
	\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install gd; \
	\
	runDeps="$( \
		scanelf --needed --nobanner --format '%n#p' --recursive /usr/local/lib/php/extensions \
			| tr ',' '\n' \
			| sort -u \
			| awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
	)"; \
	apk add --virtual .wordpress-phpexts-rundeps $runDeps; \
	apk del .build-deps

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

VOLUME /var/www/html

ENV WORDPRESS_VERSION 5.0.3
ENV WORDPRESS_SHA1 f9a4b482288b5be7a71e9f3dc9b5b0c1f881102b

RUN set -ex; \
	curl -o wordpress.tar.gz -fSL "https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz"; \
	echo "$WORDPRESS_SHA1 *wordpress.tar.gz" | sha1sum -c -; \
# upstream tarballs include ./wordpress/ so this gives us /usr/src/wordpress
	tar -xzf wordpress.tar.gz -C /usr/src/; \
	rm wordpress.tar.gz; \
	chown -R www-data:www-data /usr/src/wordpress

ENV PATH "$PATH:/usr/local/bin/"
COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint.sh / # backwards compat

# Install composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl --silent --show-error https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install nodejs & npm
run apk add automake
RUN apk add --update nodejs; \
    apk add --update npm;

# Install java
# https://github.com/sgerrand/alpine-pkg-glibc/releases - url from discussion: https://github.com/gliderlabs/docker-alpine/issues/11
# Why: install glicb release else java wont work: ibjli.so: __rawmemchr: symbol not found
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk; \
    apk add --allow-untrusted glibc-2.28-r0.apk;

ENV JAVAVER "jre1.8.0_201"
ENV JAVAPATH "/opt/java/current"
RUN apk add attr; \
#    apk add libc6-compat; \
    mkdir -p /opt/java; \
    cd /opt/java; \
    wget --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jre-8u201-linux-x64.tar.gz; \
    tar -xzf jre-8u201-linux-x64.tar.gz -C /opt/java; \
    ln -s $JAVAVER $JAVAPATH; \
    apk add paxctl; \
    cd $JAVAPATH/bin; \
    paxctl -c java; \
    paxctl -m java; \
    setfattr -n user.pax.flags -v "mr" java;

ENV JAVA_HOME=$JAVAPATH
ENV PATH=$PATH:$JAVAPATH/bin

RUN apk add py-pip;

RUN echo "TEST_URL=127.0.0.1" > .env;

ENTRYPOINT ["bash", "docker-entrypoint.sh"]
CMD ["php-fpm"]
