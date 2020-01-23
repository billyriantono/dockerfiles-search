FROM php:7.2-fpm-alpine

## steps borrowed from:
## https://github.com/getgrav/docker-grav/blob/master/Dockerfile

## define runtime packages
ENV RUNPKGS="\
  unzip \
  patch \
  libpq \
  libmemcached \
  libpng \
  libjpeg-turbo \
  libzip \
  freetype \
  yaml \
  dumb-init \
  "
## define build packages
ENV DEVPKGS="\
  freetype-dev \
  libjpeg-turbo-dev \
  libpng-dev \
  yaml-dev \
  libzip-dev \
  zlib-dev \
  autoconf \
  gcc \
  g++ \
  make \
  libmemcached-dev \
  "

## install dependencies
RUN set -ex \
    && apk add --no-cache $RUNPKGS $DEVPKGS

## patch php source against freetype-config not found bug in GD module
## source: https://stackoverflow.com/questions/57046857/freetype-config-not-found-error-when-we-install-gd-in-php7-2-apache-in-docker
ADD https://git.archlinux.org/svntogit/packages.git/plain/trunk/freetype.patch?h=packages/php /tmp/freetype.patch
RUN docker-php-source extract; \
    cd /usr/src/php; \
    patch -p1 -i /tmp/freetype.patch; \
    rm /tmp/freetype.patch

RUN set -ex \
    && docker-php-ext-install opcache

RUN set -ex \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install zip

RUN set -ex \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

## set recommended PHP.ini settings
## see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
		echo 'upload_max_filesize=128M'; \
		echo 'post_max_size=128M'; \
	} > /usr/local/etc/php/conf.d/php-recommended.ini

RUN pecl install yaml
RUN pecl install apcu
RUN docker-php-ext-enable yaml apcu

## set workdir for further downloads
WORKDIR /tmp

## take care of extensions not included in the source
RUN mkdir -p /usr/src/php/ext

## install needed php extensions: memcached
ADD http://pecl.php.net/get/memcached-3.0.3.tgz /tmp/memcached.tgz
RUN set -ex \
    && tar -xf memcached.tgz -C /usr/src/php/ext/ \
    && echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini \
    && mv /usr/src/php/ext/memcached-3.0.3 /usr/src/php/ext/memcached
RUN docker-php-ext-install memcached

## define Grav version and expected SHA1 signature as build arguments
ARG GRAV_VERSION=1.6.11
ARG GRAV_SHA1=5bad00e7884dd1792820e192433bfd1a17b1ec27
## define webroot directories for later overrides
ARG WEBROOT=/web
ARG WEBROOT_GRAV=${WEBROOT}/grav
ARG WEBROOT_GRAV_USER=${WEBROOT_GRAV}/user

## install grav
ADD https://getgrav.org/download/core/grav-admin/${GRAV_VERSION} /tmp/grav-admin.zip
RUN set -ex \
    && echo "${GRAV_SHA1}  /tmp/grav-admin.zip" | sha1sum -c - \
    && unzip -d ${WEBROOT} /tmp/grav-admin.zip \
    && mv ${WEBROOT}/grav-admin ${WEBROOT_GRAV} \
    && mv ${WEBROOT_GRAV_USER} ${WEBROOT_GRAV}/user_dist \
    && chown -R www-data:www-data ${WEBROOT}

## cleanup
RUN set -ex \
    && rm -rvf /tmp/* \
    && docker-php-source delete \
    && rm -rf /usr/src \
    && apk del --purge $DEVPKGS

## add a bunch of startup scripts with the 'last' one
## being the actual php-fpm executor
ADD runtime /runtime

## set default workdir, note: we are still running as root
WORKDIR ${WEBROOT}

## using dumb-init should give the process tree enough control over spawned children
ENTRYPOINT ["dumb-init","--"]
CMD ["run-parts","--exit-on-error","/runtime"]

# provide container image for data persistance
VOLUME ${WEBROOT}

