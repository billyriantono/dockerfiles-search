FROM ezkrg/php5-fpm:latest

ENV WORDPRESS_VERSION 4.7
ENV WORDPRESS_SHA1 1e14144c4db71421dc4ed22f94c3914dfc3b7020

RUN apk add --no-cache --update php5-gd php5-mysqli php5-opcache \
 && apk add --no-cache --virtual .build-deps openssl \
 && { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
    } > /etc/php5/conf.d/opcache-recommended.ini \
 && set -x \
 && wget -O /tmp/wordpress.tar.gz "https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz" \
 && echo "$WORDPRESS_SHA1 */tmp/wordpress.tar.gz" | sha1sum -c - \
 && tar -xzf /tmp/wordpress.tar.gz -C /var/www \
 && chown -R www-data:www-data /var/www/wordpress \
 && rm -rf /tmp/* \
 && apk del .build-deps

COPY docker-entrypoint.sh /usr/local/bin/

VOLUME [ "/var/www" ]

EXPOSE 9000

ENTRYPOINT [ "docker-entrypoint.sh" ]

CMD [ "/usr/bin/php-fpm" ]

