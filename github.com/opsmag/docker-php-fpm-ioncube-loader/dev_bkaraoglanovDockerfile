FROM alpine:3.11.2
MAINTAINER Boris Karaoglanov "boris@opsmag.com"

# ensure www-data user exists
RUN set -x \
	&& addgroup -g 82 -S www-data \
	&& adduser -u 82 -D -S -G www-data www-data

RUN echo "http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN apk --update add \
        php7-dom \
        php7-ctype \
        php7-curl \
        php7-fpm \
        php7-gd \
        php7-intl \
        php7-json \
        php7-mbstring \
	    php7-mcrypt \
        php7-mysqlnd \
        php7-opcache \
        php7-pdo \
        php7-pdo_mysql \
        php7-posix \
        php7-session \
        php7-tidy \
        php7-xml \
        php7-zip \
        php7-mysqli \
    && rm -rf /var/cache/apk/*

#Copy special configs
COPY configs/php.ini         /etc/php7/php.ini
COPY configs/php-fpm.conf    /etc/php7/php-fpm.conf
COPY configs/www.conf        /etc/php7/php-fpm.d/www.conf

# Install ioncube
RUN apk add --no-cache curl wget && \
    mkdir -p setup && cd setup && \
    wget https://kbimages.dreamhosters.com/files/ioncube_loader_lin_7.3.so && \
    mv ioncube_loader_lin_7.3.so /usr/lib/php7/modules/ioncube_loader_lin_7.3.so && \
    echo 'zend_extension = /usr/lib/php7/modules/ioncube_loader_lin_7.3.so' >  /etc/php7/conf.d/00_ioncube.ini && \
    chmod -R 777 /usr/lib/php7/modules/ioncube_loader_lin_7.3.so && \
    chown -R root:root /usr/lib/php7/modules/ioncube_loader_lin_7.3.so && \
    cd .. && rm -rf setup

WORKDIR /var/www/html

#Set port
EXPOSE 9000

CMD ["php-fpm7", "-F"]