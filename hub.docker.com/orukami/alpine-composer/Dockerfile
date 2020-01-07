FROM alpine:edge

ENV COMPOSER_HOME /composer
ENV COMPOSER_CACHE_DIR /composer/cache

ADD install-production.sh /usr/local/bin/install-production

RUN apk update && apk add php-cli php-ctype curl php-json php-openssl php-phar git && \
	curl -sS https://getcomposer.org/installer | \
	php -- --install-dir=/usr/local/bin --filename=composer	&& \
	rm -rf /var/cache/apk/* && \
	chmod +x /usr/local/bin/install-production

VOLUME ["/composer"]