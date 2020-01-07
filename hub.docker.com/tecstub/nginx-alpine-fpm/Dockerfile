FROM alpine:3.9
RUN mkdir -p /run/nginx
RUN mkdir -p /run/php/
RUN apk update \
    && apk --no-cache add nginx php-fpm php php-common php-gd php-curl php-intl php-openssl php-phar php-xmlwriter php-tokenizer php-xsl php-pdo php-mbstring php-zip php-bcmath php-iconv php-soap php7-pear php7-dev supervisor alpine-sdk openssl-dev php-json \
    && rm -rf /var/cache/apk/*
RUN pecl install mongodb \
    && pecl clear-cache
ADD https://getcomposer.org/download/1.8.0/composer.phar /bin/composer
RUN chmod +rx /bin/composer
RUN echo "extension=mongodb.so" > /etc/php7/conf.d/mongodb.ini
RUN sed -i 's/zlib.output_compression = Off/zlib.output_compression = On/' /etc/php7/php.ini
COPY conf/supervisord.conf /etc/supervisord.conf
COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY conf/fpm.conf /etc/nginx/conf.d/default.conf
COPY pub/index.php /var/www/html/pub/index.php
COPY scripts/. /bin/
RUN ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log
RUN chown -R nginx:nginx /var/www
CMD ["/usr/bin/supervisord"]
