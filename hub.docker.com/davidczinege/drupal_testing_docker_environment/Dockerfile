# from https://www.drupal.org/requirements/php#drupalversions
FROM php:7.1-apache
MAINTAINER David Czinege

ENV DEBIAN_FRONTEND noninteractive

RUN a2enmod rewrite

# install the PHP extensions we need
RUN set -ex \
	&& buildDeps=' \
		libjpeg62-turbo-dev \
		libpng12-dev \
		libpq-dev \
	' \
	&& apt-get update && apt-get install -y --no-install-recommends $buildDeps && rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd \
		--with-jpeg-dir=/usr \
		--with-png-dir=/usr \
	&& docker-php-ext-install -j "$(nproc)" gd mbstring opcache pdo pdo_mysql pdo_pgsql zip \
# PHP Warning:  PHP Startup: Unable to load dynamic library '/usr/local/lib/php/extensions/no-debug-non-zts-20151012/gd.so' - libjpeg.so.62: cannot open shared object file: No such file or directory in Unknown on line 0
# PHP Warning:  PHP Startup: Unable to load dynamic library '/usr/local/lib/php/extensions/no-debug-non-zts-20151012/pdo_pgsql.so' - libpq.so.5: cannot open shared object file: No such file or directory in Unknown on line 0
	&& apt-mark manual \
		libjpeg62-turbo \
		libpq5 \
	&& apt-get purge -y --auto-remove $buildDeps

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

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini && \
  echo "date.timezone=America/Chicago" > $PHP_INI_DIR/conf.d/date_timezone.ini && \
  echo "sendmail_path=/bin/true" > $PHP_INI_DIR/conf.d/sendmail.ini

# Adding the official Oracle MySQL APT repositories to install MySQL 5.6 (including the apt-get key)
RUN apt-key adv --keyserver keys.gnupg.net --recv-keys 5072E1F5
RUN echo "deb http://repo.mysql.com/apt/debian/ jessie mysql-5.6" >> /etc/apt/sources.list

RUN \
 echo "mysql-server mysql-server/root_password password root" | debconf-set-selections &&\
 echo "mysql-server mysql-server/root_password_again password root" | debconf-set-selections

# Install some other dependencies:
# - libfreetype6-dev -  FreeType 2 font engine, shared library files
#  libjpeg62-turbo-dev - The libjpeg-turbo JPEG library is a library for handling JPEG files.
#  libmcrypt-dev - Libmcrypt is a thread-safe library providing a uniform interface to access several block and stream encryption algorithms.
#  libpng12-dev - libpng is a library implementing an interface for reading and writing PNG (Portable Network Graphics) format files.
#  libbz2-dev - high-quality block-sorting file compressor library
#  php-pear - PEAR - PHP Extension and Application Repository
#  curl - this allows you to connect and communicate to many different types of servers with many different types of protocols.
#  git - version control system
#  mysql client
#  mysql server
#  unzip - compression manager
#  && docker-php-ext-install mcrypt zip bz2 bcmath pdo_mysql mysqli mbstring opcache - install php extensisons
#  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#  && docker-php-ext-install gd
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libpng12-dev \
  libbz2-dev \
  php-pear \
  curl \
  git \
  unzip \
  && docker-php-ext-install mcrypt zip bz2 bcmath pdo_mysql mysqli mbstring opcache \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd

# Install MySQL
RUN apt-get update \
  && apt-get install -y mysql-server mysql-client libmysqlclient-dev --no-install-recommends \
  && docker-php-ext-install pdo pdo_mysql \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Composer and PHPUnit
RUN \
 curl -sSL https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/bin &&\
 curl -sSL https://phar.phpunit.de/phpunit-5.7.phar -o /usr/bin/phpunit  && chmod +x /usr/bin/phpunit  &&\
 rm -rf /root/.npm /root/.composer /tmp/* /var/lib/apt/lists/*

# Install Drush 8 and coder (codesniffer).
RUN composer global require drush/drush:8.* drupal/coder &&\
 composer global update &&\
 ln -s /root/.composer/vendor/bin/drush /usr/local/bin/drush &&\
 ln -s /root/.composer/vendor/bin/phpcs /usr/local/bin/phpcs &&\
 phpcs --config-set installed_paths ~/.composer/vendor/drupal/coder/coder_sniffer

VOLUME /var/www/html
WORKDIR /var/www/html
