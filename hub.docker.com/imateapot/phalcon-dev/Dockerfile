FROM imateapot/phalcon-pgsql

ENV COMPOSER_CACHE_DIR=/tmp/composer-cache

RUN set -ex \
	&& docker-phalcon-install-devtools \
	&& stable_version=$(curl -s https://getcomposer.org/ | grep -o "Latest: v[0-9]*\.[0-9]*\.[0-9]*" | sed "s/Latest: v//") \
	&& wget https://getcomposer.org/download/$stable_version/composer.phar -O /usr/local/bin/composer \
	&& chmod +x /usr/local/bin/composer
