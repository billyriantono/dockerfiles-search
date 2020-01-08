FROM debian:jessie
MAINTAINER Cees-Jan Kiewiet <hi@ceesjankiewiet.nl>

# Install build requirements
# ...then compile PHP & the pthreads extension
# ...then do some cleanup

RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y \
		autoconf \
		build-essential \
		libssl-dev \
		libxml2-dev \
		wget \

	&& wget -qO php-7.0.17.tar.bz2 http://us1.php.net/get/php-7.0.17.tar.bz2/from/this/mirror \
	&& tar xjf php-7.0.17.tar.bz2 \
	&& cd php-7.0.17 \
	&& ./configure \
		--disable-cgi \
		--enable-mbstring \
		--enable-maintainer-zts \
		--enable-zip \
		--with-libdir=/lib/x86_64-linux-gnu \
		--with-openssl \
	&& make \
	&& make install \
	&& cp php.ini-production /usr/local/lib/php.ini \
	&& sed -i "s/^;date.timezone =$/date.timezone = \"UTC\"/" /usr/local/lib/php.ini \
	&& cd .. \
	&& pecl config-set php_ini /usr/local/lib/php.ini \
	&& pear config-set php_ini /usr/local/lib/php.ini \
	&& pecl install pthreads \

	&& rm php-7.0.17.tar.bz2 \
	&& rm -rf php-7.0.17 \
	&& apt-get purge -y autoconf build-essential wget .+-dev \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT ["php"]
CMD ["--help"]
