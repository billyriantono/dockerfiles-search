FROM usijo/docker-alpine:3.5
MAINTAINER Hongshun Yang<ojisucom@gmail.com>

RUN apk add -U php7 \
php7-calendar \
php7-bcmath \
php7-bz2 \
php7-cgi \
php7-common \
php7-ctype \
php7-curl \
php7-dba \
php7-dev \
php7-dom \
php7-embed \
php7-enchant \
php7-exif \
php7-fpm \
php7-gd \
php7-gettext \
php7-gmp \
php7-iconv \
php7-imap \
php7-intl \
php7-json \
php7-mcrypt \
php7-mysqli \
php7-mbstring \
php7-opcache \
php7-openssl \
php7-pcntl \
php7-pdo \
php7-pdo_dblib \
php7-pdo_mysql \
php7-pear \
php7-phar \
php7-phpdbg \
php7-posix \
php7-session \
php7-shmop \
php7-soap \
php7-sockets \
php7-sysvmsg \
php7-sysvsem \
php7-sysvshm \
php7-xml \
php7-xmlreader \
php7-xmlrpc \
php7-xsl \
php7-zip \
php7-zlib \
php7-apcu 


RUN sed -i "$ s|\-n||g" /usr/bin/pecl

RUN apk -U add geoip \
&& apk add --virtual build-deps geoip-dev autoconf build-base linux-headers git libtool \
&& cd /tmp/ \
&& git clone https://github.com/php7-extensions/ext-php7-geoip.git \
&& cd ext-php7-geoip \
&& phpize7 && ./configure --with-php-config=/usr/bin/php-config7 && make && make install \
&& rm -rf /tmp/* \
&& apk del -U build-deps \
&& rm -rf /var/cache/apk/*

RUN echo "extension=geoip.so" > /etc/php7/conf.d/geoip.ini \
&& echo "geoip.custom_directory=/usr/share/GeoIP" >> /etc/php7/conf.d/geoip.ini
## listen [::]:9000
#COPY tmpl/_etc_php7_php-fpm.conf.tmpl /etc/php7/php-fpm.conf.tmpl

COPY rootfs/_usr_share_GeoIP /usr/share/GeoIP

RUN mkdir -p /var/www/html

VOLUME /var/www/html

EXPOSE 9000
#todo log
## --nodaemonize
CMD ["php-fpm7","-F"]

