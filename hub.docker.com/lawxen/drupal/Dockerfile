FROM lawxen/drupal:8-fpm-nginx

# Install xdebug
RUN pecl install xdebug && docker-php-ext-enable xdebug

# Xdebug config
ENV XDEBUG_ENABLE 0
ENV XDEBUG_REMOTE_ENABLE 1
ENV XDEBUG_REMOTE_AUTOSTART 1
ENV XDEBUG_MAX_NESTING_LEVEL 200
ENV XDEBUG_REMOTE_HOST 127.0.0.1
ENV XDEBUG_REMOTE_PORT 9001
ENV XDEBUG_IDEKEY PHPSTORM
RUN if [ "$XDEBUG_ENABLE" = "1" ]; then \
	{ \
	echo '[xdebug]'; \
	echo 'xdebug.remote_enable= $XDEBUG_REMOTE_ENABLE'; \
	echo 'xdebug.remote_autostart = $XDEBUG_REMOTE_AUTOSTART'; \
	echo 'xdebug.max_nesting_level = $XDEBUG_MAX_NESTING_LEVEL'; \
	echo 'xdebug.remote_handler = dbgp'; \
	echo 'xdebug.remote_host = $XDEBUG_REMOTE_HOST'; \
	echo 'xdebug.remote_port = $XDEBUG_REMOTE_PORT'; \
	echo 'xdebug.idekey = $XDEBUG_IDEKEY'; \
	} > /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
	else \
	sed -i '1d' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
	fi