FROM buildpack-deps:jessie
MAINTAINER Eugene Ware <eugene@noblesamurai.com>

RUN apt-get update

RUN apt-get install -y \
    libxml2-dev \
    libjpeg-dev \
    libpng-dev \
    libxpm-dev \
    libpq-dev \
    libicu-dev \
    libfreetype6-dev \
    libldap2-dev \
    libxslt-dev \
    libmcrypt-dev \
    libldb-dev \
    build-essential \
    libmysqlclient-dev \
    libcurl4-gnutls-dev \
    curl \
    && rm -r /var/lib/apt/lists/*


##<apache2>##
RUN apt-get update && apt-get install -y apache2-bin apache2-dev apache2.2-common --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN rm -rf /var/www/html && mkdir -p /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www/html && chown -R www-data:www-data /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www/html

# Apache + PHP requires preforking Apache for best results
RUN a2dismod mpm_event && a2enmod mpm_prefork && a2enmod rewrite && a2enmod headers

RUN mv /etc/apache2/apache2.conf /etc/apache2/apache2.conf.dist
COPY apache2.conf /etc/apache2/apache2.conf
##</apache2>##

RUN mkdir /usr/include/freetype2/freetype
RUN ln -s /usr/include/freetype2/freetype.h /usr/include/freetype2/freetype/freetype.h

#RUN gpg --keyserver pgp.mit.edu --recv-keys 0B96609E270F565C13292B24C13C70B87267B52D 0A95E9A026542D53835E3F3A7DEC4E69FC9C83D7

ENV GPG_KEYS 0B96609E270F565C13292B24C13C70B87267B52D 0A95E9A026542D53835E3F3A7DEC4E69FC9C83D7 0E604491
RUN set -xe \
  && for key in $GPG_KEYS; do \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
  done

# compile openssl, otherwise --with-openssl won't work
RUN CFLAGS="-fPIC" && OPENSSL_VERSION="1.0.2d" \
      && cd /tmp \
      && mkdir openssl \
      && curl -sL "https://www.openssl.org/source/openssl-$OPENSSL_VERSION.tar.gz" -o openssl.tar.gz \
      && curl -sL "https://www.openssl.org/source/openssl-$OPENSSL_VERSION.tar.gz.asc" -o openssl.tar.gz.asc \
      && gpg --verify openssl.tar.gz.asc \
      && tar -xzf openssl.tar.gz -C openssl --strip-components=1 \
      && cd /tmp/openssl \
      && ./config shared && make && make install \
      && rm -rf /tmp/*

ENV PHP_VERSION 5.3.29

ENV PHP_INI_DIR /usr/local/lib
RUN mkdir -p $PHP_INI_DIR/conf.d


RUN ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so
RUN ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so

# php 5.3 needs older autoconf
RUN set -x \
	&& apt-get update && apt-get install -y autoconf2.13 && rm -r /var/lib/apt/lists/* \
	&& curl -SLO http://launchpadlibrarian.net/140087283/libbison-dev_2.7.1.dfsg-1_amd64.deb \
	&& curl -SLO http://launchpadlibrarian.net/140087282/bison_2.7.1.dfsg-1_amd64.deb \
	&& dpkg -i libbison-dev_2.7.1.dfsg-1_amd64.deb \
	&& dpkg -i bison_2.7.1.dfsg-1_amd64.deb \
	&& rm *.deb \
	&& curl -SL "http://php.net/get/php-$PHP_VERSION.tar.bz2/from/this/mirror" -o php.tar.bz2 \
	&& curl -SL "http://php.net/get/php-$PHP_VERSION.tar.bz2.asc/from/this/mirror" -o php.tar.bz2.asc \
	&& gpg --verify php.tar.bz2.asc \
	&& mkdir -p /usr/src/php \
	&& tar -xf php.tar.bz2 -C /usr/src/php --strip-components=1 \
	&& rm php.tar.bz2* \
	&& cd /usr/src/php \
	&& ./buildconf --force \
	&& ./configure --disable-cgi \
		$(command -v apxs2 > /dev/null 2>&1 && echo '--with-apxs2' || true) \
    --with-config-file-path="$PHP_INI_DIR" \
    --with-config-file-scan-dir="$PHP_INI_DIR/conf.d" \
		--with-mysql \
		--with-mysqli \
		--with-pdo-mysql \
		--with-mbstring \
        --enable-mbstring \
		--with-openssl=/usr/local/ssl \
		--with-mcrypt \
		--with-memcached \
		--with-sockets \
		--with-dba \
		--with-zib \
        --with-zlib \
        --enable-zip \
        --with-gd \
        --with-png-dir=/usr/lib/x86_64-linux-gnu \
        --with-jpeg-dir=/usr/lib/x86_64-linux-gnu \
        --enable-gd-native-ttf \
        --with-freetype-dir \
        --with-xsl \
        --with-ldap \
        --with-soap \
		--with-gettext \
        --with-xml \
        --with-xmlrpc \
        --with-curl \
        --enable-soap \
        --enable-cli \
        --enable-libxml \
        --enable-session \
        --enable-xml \
        --enable-simplexml \
        --enable-filter \
        --enable-inline-optimization \
        --enable-exif \
        --enable-soap \
        --enable-dba \
        --enable-curl \
        --enable-sockets \
        --enable-memcached \
        --enable-bcmath \
        --enable-bz2 \
        --enable-calendar \
	&& make -j"$(nproc)" \
	&& make install \
	&& dpkg -r bison libbison-dev \
	&& apt-get purge -y --auto-remove autoconf2.13 \
  && make clean


COPY docker-php-* /usr/local/bin/
COPY apache2-foreground /usr/local/bin/

RUN pear upgrade-all
RUN pear install System_Daemon
RUN mkdir /var/log/reports-daemon

WORKDIR /var/www/html

EXPOSE 80
CMD ["apache2-foreground"]
