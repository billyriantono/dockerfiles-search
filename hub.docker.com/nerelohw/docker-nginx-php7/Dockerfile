FROM nerelohw/docker-nginx
LABEL MAINTAINER="wholerencom@gmail.com"


RUN setup-alpine-mirror -c us \
&& apk add -U --force php7 \
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
php7-apcu \
php7-redis \
php7-memcached \
php7-imagick \
php7-fileinfo \
php7-xmlwriter \
php7-simplexml \
php7-ldap \
php7-ftp \
php7-xdebug \
php7-tokenizer
#php7-gmagick@edge_testing

RUN sed -i "$ s|\-n||g" /usr/bin/pecl

# not working
#ENV PECL_GMAGICK_VERSION 2.0.4RC1
#&& pecl install gmagick-$PECL_GMAGICK_VERSION \

RUN apk -U --force add geoip yaml graphicsmagick 
RUN apk -U --force add --virtual build-deps geoip-dev autoconf build-base linux-headers git libtool yaml-dev graphicsmagick-dev \
&& pecl install yaml \
&& cd /tmp/ \
&& git clone https://github.com/php7-extensions/ext-php7-geoip.git \
&& cd ext-php7-geoip \
&& phpize7 && ./configure --with-php-config=/usr/bin/php-config7 && make && make install \
&& rm -rf /tmp/* \
&& apk -U --force del build-deps \
&& rm -rf /var/cache/apk/*

#&& echo "extension=gmagick.so" > /etc/php7/conf.d/gmagick.ini \
RUN echo "extension=geoip.so" > /etc/php7/conf.d/geoip.ini \
&& echo "extension=yaml.so" > /etc/php7/conf.d/yaml.ini \
&& echo "geoip.custom_directory=/usr/share/GeoIP" >> /etc/php7/conf.d/geoip.ini \
&& sed -i 's/127.0.0.1:9000/9000/g' /etc/php7/php-fpm.d/www.conf
## listen [::]:9000
#COPY tmpl/_etc_php7_php-fpm.conf.tmpl /etc/php7/php-fpm.conf.tmpl

COPY rootfs/_usr_share_GeoIP /usr/share/GeoIP
COPY rootfs/_usr_local_bin/composer-installer /usr/local/bin/composer-installer

RUN chmod a+x /usr/local/bin/* \
&& cd /tmp/ \
&& composer-installer \
&& mv composer.phar /usr/local/bin/composer \
&& mkdir -p /var/www/html

VOLUME ["/var/www/html","/tmp"]

EXPOSE 80 443 9000

CMD ["php-fpm7","-F"]

