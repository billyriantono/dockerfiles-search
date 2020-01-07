FROM wodby/php:5.6
MAINTAINER Romash <tcp6000@gmail.com>

ENV INSTALL_PATH="/var/www/html" \
    PHP_ALWAYS_POPULATE_RAW_POST_DATA="-1" \
    PHP_MBSTRING_ENCODING_TRANSLATION="Off" \
    PHP_MBSTRING_HTTP_INPUT="pass" \
    PHP_MBSTRING_HTTP_OUTPUT="pass" \
    PHP_OUTPUT_BUFFERING="16384" \
    PHP_REALPATH_CACHE_SIZE="64k" \
    PHP_REALPATH_CACHE_TTL="3600" \
    PHP_SESSION_AUTO_START="0"

RUN apk add --update dovecot
RUN set -xe \
	&& apk add --no-cache --virtual .gettext-deps \
		gettext-dev \
	\
	&& cd /usr/src \
	&& wget -O php.tar.xz "$PHP_URL" \
	&& docker-php-ext-install gettext \
	&& cd / \
	&& docker-php-source delete \
	&& apk del .gettext-deps

RUN su-exec www-data composer -n create-project opensolutions/vimbadmin $INSTALL_PATH -s dev
RUN cp $INSTALL_PATH/public/.htaccess.dist $INSTALL_PATH/public/.htaccess

COPY templates /etc/gotpl/
COPY init/* /docker-entrypoint-init.d/
