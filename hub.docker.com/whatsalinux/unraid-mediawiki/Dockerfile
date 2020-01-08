FROM php:7.2-apache

# System Dependencies.
RUN echo "step 1" > /opt/progress
RUN apt-get update && apt-get install -y \
		git \
		imagemagick \
		libicu-dev \
		# Required for SyntaxHighlighting
		python3 \
	--no-install-recommends && rm -r /var/lib/apt/lists/*

# Install the PHP extensions we need
RUN echo "step 2" >> /opt/progress
RUN docker-php-ext-install mbstring mysqli opcache intl

# Install the default object cache.
RUN echo "step 3" >> /opt/progress
RUN pecl channel-update pecl.php.net \
	&& pecl install apcu \
	&& docker-php-ext-enable apcu

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN echo "step 4" >> /opt/progress
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=60'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

# SQLite Directory Setup
RUN echo "step 5" >> /opt/progress
RUN mkdir -p /var/www/data \
	&& chown -R www-data:www-data /var/www/data

# Version
ENV MEDIAWIKI_MAJOR_VERSION 1.31
ENV MEDIAWIKI_BRANCH REL1_31
ENV MEDIAWIKI_VERSION 1.31.1
ENV MEDIAWIKI_SHA512 ee49649cc37d0a7d45a7c6d90c822c2a595df290be2b5bf085affbec3318768700a458a6e5b5b7e437651400b9641424429d6d304f870c22ec63fae86ffc5152

# MediaWiki setup
RUN echo "step 6" >> /opt/progress
WORKDIR /var/www/html
RUN curl -fSL "https://releases.wikimedia.org/mediawiki/${MEDIAWIKI_MAJOR_VERSION}/mediawiki-${MEDIAWIKI_VERSION}.tar.gz" -o mediawiki.tar.gz
RUN tar -xz --strip-components=1 -f mediawiki.tar.gz
RUN chown -R www-data:www-data extensions skins cache images
#end
