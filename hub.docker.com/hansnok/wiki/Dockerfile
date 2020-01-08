FROM php:7.1-apache

# install the PHP extensions we need
RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y \
		libjpeg-dev \
		libpng-dev \
		libbz2-dev \
		zlib1g-dev \
		unzip \
	; \
	rm -rf /var/lib/apt/lists/*; \
	\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install gd mysqli opcache
# TODO consider removing the *-dev deps and only keeping the necessary lib* packages

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

RUN a2enmod rewrite expires

VOLUME /var/www/html

ENV WORDPRESS_VERSION 4.9.6
ENV WORDPRESS_SHA1 40616b40d120c97205e5852c03096115c2fca537
ENV KNOWLEDGEBASE_VERSION 1.1.8
ENV IXION_VERSION 1.1.2
ENV TABLEPRESS_VERSION 1.9
ENV WPO365_VERSION 4.2

RUN set -ex; \
	curl -o wordpress.tar.gz -fSL "https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz"; \
	echo "$WORDPRESS_SHA1 *wordpress.tar.gz" | sha1sum -c -; \
# upstream tarballs include ./wordpress/ so this gives us /usr/src/wordpress
	tar -xzf wordpress.tar.gz -C /usr/src/; \
	rm wordpress.tar.gz; \
# Add wp-knowledgebase plugin
	curl -o knowledgebase.tar.gz -fSL "https://github.com/maevelander/wp-knowledgebase/archive/${KNOWLEDGEBASE_VERSION}.tar.gz"; \
	tar -xzf knowledgebase.tar.gz -C /usr/src/wordpress/wp-content/plugins/; \
	rm knowledgebase.tar.gz; \
# Add TablePress plugin
	curl -o tablepress.zip -fSL "https://downloads.wordpress.org/plugin/tablepress.${TABLEPRESS_VERSION}.zip"; \
	unzip tablepress.zip -d /usr/src/wordpress/wp-content/plugins/; \
	rm tablepress.zip; \
# Add WPO365 plugin
	curl -o wpo365.zip -fSL "https://downloads.wordpress.org/plugin/wpo365-login.zip"; \
	unzip wpo365.zip -d /usr/src/wordpress/wp-content/plugins/; \
	rm wpo365.zip; \
# Add Ixion theme
	curl -o ixion.zip -fSL "https://downloads.wordpress.org/theme/ixion.${IXION_VERSION}.zip"; \
	unzip ixion.zip -d /usr/src/wordpress/wp-content/themes/; \
	rm ixion.zip; \
# Add Spanish languague to Wordpress
	curl -o wordpress.tar.gz -fSL "https://es.wordpress.org/wordpress-${WORDPRESS_VERSION}-es_ES.tar.gz"; \
	mkdir /usr/src/temp/; \
	tar -xzf wordpress.tar.gz -C /usr/src/temp/; \
	rm wordpress.tar.gz; \
	cp -R /usr/src/temp/wordpress/wp-content/languages/ /usr/src/wordpress/wp-content/; \
	rm -R  /usr/src/temp; \
	chown -R www-data:www-data /usr/src/wordpress;

COPY docker-entrypoint.sh /usr/local/bin/

RUN chmod 777 /usr/local/bin/docker-entrypoint.sh \
    && ln -s /usr/local/bin/docker-entrypoint.sh /

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]