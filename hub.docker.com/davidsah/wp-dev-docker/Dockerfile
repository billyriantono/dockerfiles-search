FROM visiblevc/wordpress:latest-php7.2

# Make sure we're root - visiblevc switches to admin
USER root

# Install global utils
RUN apt-get update && apt-get install -y git

# Install xDebug
RUN pecl install xdebug-2.6.0 \
	&& docker-php-ext-enable xdebug

# Configgure xDebug
RUN echo "xdebug.remote_enable = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_autostart = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_host = docker.for.mac.localhost" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_port = 9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_log = /app/xdebug.log" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.idekey = VSCODE" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Install code sniffer
RUN pear install pear/PHP_CodeSniffer

# Checkout Wordpress standards (0.10.0)
RUN git clone git://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards.git $(pear config-get php_dir)/PHP/CodeSniffer/Standards/WordPress && \
    (cd $(pear config-get php_dir)/PHP/CodeSniffer/Standards/WordPress; git checkout tags/0.10.0) && \
    phpcs --config-set installed_paths $(pear config-get php_dir)/PHP/CodeSniffer/Standards/WordPress && \
    phpcs --config-set default_standard WordPress

# Cleanup
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER admin
