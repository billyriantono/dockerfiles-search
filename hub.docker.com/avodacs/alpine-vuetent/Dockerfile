FROM alpine
MAINTAINER Andreas Peters <noreply@aventer.biz>

WORKDIR /var/www/html

RUN set -xe \
    && apk add --no-cache ca-certificates \
                          gzip \
                          nginx \
                          openssl \
                          php5-fpm \
                          php5-openssl \
                          php5-pdo_sqlite \
                          php5-sqlite3 \
                          php5-xml \
                          php5-zlib \
                          php5-mysql \
                          php5-gd \
                          php5-curl \
                          php5-zip \
                          php5-iconv \
                          php5-json \                          
                          php5-dom \                          
			              curl \
                          tar \
    && touch /etc/php5/fpm.d/empty.conf \
    && curl -R -L -O "http://repository.rainloop.net/v2/webmail/rainloop-latest.zip" \
    && unzip rainloop-latest.zip -d /var/www/html/ \
    && chown -R nobody:nobody .

COPY nginx.conf /etc/nginx/nginx.conf

VOLUME /var/www/html

EXPOSE 8888

CMD php-fpm5 && nginx -g 'daemon off;'
