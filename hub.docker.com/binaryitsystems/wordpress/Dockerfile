FROM wordpress:5
MAINTAINER Binary IT Systems LLC

RUN apt-get update \
    && apt-get install -y \
		curl \
		jq \
		less \
		vim \
		unzip \
        wget \
        libxml2-dev \
        libjpeg-dev \
        libmemcached-dev \
        libpng-dev \
    && rm -rf /var/lib/apt/lists/* \
    && pecl install memcached-3.1.3 \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install gd opcache soap \
    && docker-php-ext-enable memcached \
	&& { \
        echo 'opcache.memory_consumption=128'; \
        echo 'opcache.interned_strings_buffer=8'; \
        echo 'opcache.max_accelerated_files=4000'; \
        echo 'opcache.revalidate_freq=60'; \
        echo 'opcache.fast_shutdown=1'; \
        echo 'opcache.enable_cli=1'; \
    } > /usr/local/etc/php/conf.d/opcache-recommended.ini

# Install wp-cli, http://wp-cli.org
ENV WP_CLI_CONFIG_PATH /var/www/html/wp-cli.yml
RUN set -ex \
    && curl --retry 7 --fail -Ls -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp \
    && wp --info --allow-root

# Install HyperDB, https://wordpress.org/plugins/hyperdb
# Releases at https://wordpress.org/plugins/hyperdb/developers/ , though no SHA1 fingerprints are published
RUN set -ex \
    && export HYPERDB_VERSION=1.5 \
    && curl --retry 7 --fail -Ls -o /var/www/html/hyperdb.zip https://downloads.wordpress.org/plugin/hyperdb.${HYPERDB_VERSION}.zip \
    && unzip hyperdb.zip \
    && chown -R www-data:www-data /var/www/html/hyperdb \
    && mv hyperdb/db.php /var/www/html/. \
    && rm -rf /var/www/html/hyperdb.zip /var/www/html/hyperdb

COPY db-config.php /var/www/html/db-config.php
    
RUN set -ex \
    && curl --retry 7 --fail -Ls -o /var/www/html/object-cache.php https://raw.githubusercontent.com/tollmanz/wordpress-pecl-memcached-object-cache/master/object-cache.php
