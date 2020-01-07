# Includes
# -----------------------------
# OS: Ubuntu
# Apps: Java
# Apps: Node.js, Gulp, Bower, Grunt, Yeoman
# Apps: Ruby, Rails, Sass, Compass
# Apps: Python
# Apps: PHP, Apache
# Apps: Wordpress
FROM jsneed/ubuntu-jre-nodejs-rails-python-php

# https://hub.docker.com/_/wordpress/
# https://github.com/docker-library/wordpress/blob/6afa0720da89f31d6c61fd38bb0d6de6e9a14a49/apache/Dockerfile

USER root
RUN a2enmod rewrite expires

# install the PHP extensions we need
RUN apt-get update \
	&& apt-get install -y libpng12-dev libjpeg-dev \
	&& rm -rf /var/lib/apt/lists/* \
	&& cd /usr/local/bin \
	&& chmod ug+rwx docker-php-ext-* \
	&& sudo sh docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& sudo sh docker-php-ext-install gd mysqli opcache \
	&& cd /var/www/html

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=60'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

#VOLUME /var/www/html

ENV WORDPRESS_VERSION 4.5.3
ENV WORDPRESS_SHA1 835b68748dae5a9d31c059313cd0150f03a49269

# upstream tarballs include ./wordpress/ so this gives us /usr/src/wordpress
RUN curl -o wordpress.tar.gz -SL https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz \
	&& echo "$WORDPRESS_SHA1 *wordpress.tar.gz" | sha1sum -c - \
	&& tar -xzf wordpress.tar.gz -C /usr/src/ \
	&& rm wordpress.tar.gz \
	&& chown -R www-data:www-data /usr/src/wordpress
USER user

COPY docker-entrypoint.sh /entrypoint.sh

# grr, ENTRYPOINT resets CMD now
ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2-foreground"]

USER user
WORKDIR /projects
CMD tail -f /dev/null