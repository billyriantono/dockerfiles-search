FROM alpine:3.7

# ensure www-data user exists
RUN set -x ; \
  addgroup -g 82 -S www-data ; \
  adduser -u 82 -D -S -G www-data www-data && exit 0 ; exit 1

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \ 
    apk update && \ 
    apk upgrade && \ 
    apk add --update \ 
    php7 \
    php7-mcrypt \ 
    php7-soap \ 
    php7-openssl \ 
    php7-gmp \ 
    php7-json \ 
    php7-dom \ 
    php7-pdo \ 
    php7-zip \ 
    php7-mysqli \ 
    php7-bcmath \ 
    php7-gd \ 
    php7-pdo_mysql \ 
    php7-gettext \ 
    php7-xmlreader \ 
    php7-xmlrpc \ 
    php7-bz2 \ 
    php7-iconv \ 
    php7-curl \
    php7-session \
    php7-fpm \
    php7-ctype \
    php7-imagick \
    php7-intl \
    php7-mbstring \
    php7-simplexml \
    php7-xml \
    php7-xsl \
    php7-phar php7-xmlwriter php7-tokenizer
    
RUN apk add \
  bash shadow nginx ca-certificates curl zip && \
  apk add -u musl && \
  mkdir -p /etc/nginx/conf.d

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

ADD files/nginx.conf /etc/nginx/
ADD files/php-fpm.conf /etc/php7/
ADD files/default.conf /etc/nginx/conf.d/
ADD files/run.sh /
RUN chmod +x /run.sh

EXPOSE 80

WORKDIR /var/www/html
VOLUME ["/var/htdocs", "/var/logs"]

CMD ["/run.sh"]

