FROM php:7.3.2-cli-alpine3.9

RUN apk add --no-cache --update postgresql-dev libssh2-dev libstdc++ && \
	apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS linux-headers && \
	pecl install redis && \
	pecl install swoole && \
    	docker-php-ext-enable swoole && \
	docker-php-ext-enable redis && \
	docker-php-source delete && \
	docker-php-ext-install pdo pdo_pgsql && \
	apk del .phpize-deps && \
	rm -rf /var/cache/apk/*

COPY php.ini /usr/local/etc/php/php.ini
EXPOSE 8080
ENTRYPOINT ["php", "-f", "/source/cli.php"]
CMD ["ping"]
