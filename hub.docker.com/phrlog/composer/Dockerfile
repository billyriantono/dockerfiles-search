FROM php:7.4.0alpha2-cli-buster

# Copy composer installer
ADD https://getcomposer.org/installer /tmp/installer
ADD https://composer.github.io/snapshots.pub /var/www/.composer/keys.dev.pub
ADD https://composer.github.io/releases.pub /var/www/.composer/keys.tags.pub

# Prepare composer dir
RUN chmod -R 777 /var/www/.composer \
	# Install packages needed for PHP
	&& apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -yqq --no-install-recommends \
		openssh-client \
		gnupg \
		unzip \
		git

# Install Composer
RUN php /tmp/installer --no-ansi --install-dir=/usr/local/bin --filename=composer \
	# Cleanup
	&& apt-get clean \
	&& rm -rf /var/tmp/* /tmp/* \
		/var/lib/apt/lists/* \
		/var/log/apt/* \
		/var/cache/debconf \
		/var/cache/apt/archives/*

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["composer"]

WORKDIR /var/www/html/
