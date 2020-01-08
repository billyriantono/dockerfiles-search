# Debian
FROM php:fpm 
MAINTAINER JimyRyan

#################################################################################
#################################################################################
#                                                                               #
#                [START :: TIMEZONE, LOCALE & UPDATE / UPGRADE]                 #
#                                                                               #
#################################################################################

RUN apt-get update -y \
    && apt-get install -y locales

# Set locale and timezone 
ENV LANGUAGE fr_FR.UTF-8
ENV LANG fr_FR.UTF-8
ENV LC_ALL fr_FR.UTF-8
ENV TZ Europe/Paris

# Change locale and timezone 
RUN set -x \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# '$LANG' UTF-8/'$LANG' UTF-8/' /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=$LANG \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone

# Update distribution
RUN apt-get update \
    && apt-get upgrade -y

#################################################################################
#                                                                               #
#                   [END :: TIMEZONE, LOCALE & UPDATE / UPGRADE]                #
#                                                                               #
#################################################################################
#################################################################################

# install the PHP extensions we need
RUN apt-get install -y libpng12-dev libjpeg-dev \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install gd mysqli opcache 

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

VOLUME /var/www/html

ENV WORDPRESS_VERSION 4.4.2
ENV WORDPRESS_SHA1 7444099fec298b599eb026e83227462bcdf312a6

# upstream tarballs include ./wordpress/ so this gives us /usr/src/wordpress
RUN curl -o wordpress.tar.gz -SL https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz \
	&& echo "$WORDPRESS_SHA1 *wordpress.tar.gz" | sha1sum -c - \
	&& tar -xzf wordpress.tar.gz -C /usr/src/ \
	&& rm wordpress.tar.gz \
	&& chown -R www-data:www-data /usr/src/wordpress

COPY ./data/docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh


#################################################################################
#################################################################################
#                                                                               #
#                           [START :: CUSTOM BUILD]                             #
#                                                                               #
#################################################################################
#
# Note : remove the "rm -rf /var/lib/apt/lists/*" command from the default Dockerfile.
#

# Wordpress config
ENV WORDPRESS_SECURE true
ENV WORDPRESS_MAIN_DOMAIN www.example.com
ENV WORDPRESS_STATIC_DOMAIN static.cdn.com

# Install php extensions and dependencies
RUN set -x \
    && buildDeps=" \
        # For mcrypt
		libmcrypt-dev \	
        # For Tidy
        libtidy-dev \
	"; \
    buildExt=" \
        mcrypt \
        mbstring \
        tidy \
    "; \
	apt-get install -y $buildDeps --no-install-recommends \
    && docker-php-ext-install -j$(nproc) $buildExt

# Set the php timezone
RUN echo 'date.timezone='$TZ > /usr/local/etc/php/conf.d/date.ini

# Copy php config files
COPY ./data/etc/php/conf.d/*.ini /usr/local/etc/php/conf.d/
RUN chmod 644 /usr/local/etc/php/conf.d/*

# Copy apply security script
COPY ./data/apply-security.sh /apply-security_entrypoint-launcher.sh
RUN chmod +x /apply-security_entrypoint-launcher.sh

# Add default robots.txt
COPY ./data/var/www/html/robots.txt /tmp/

# Add wp-myconfig.php
COPY ./data/var/www/html/wordpress/wp-myconfig.php /tmp/wp-myconfig.php

VOLUME /var/log/php

# Remove the apt list
RUN rm -rf /var/lib/apt/lists/* 

#################################################################################
#                                                                               #
#                               [END :: CUSTOM BUILD]                           #
#                                                                               #
#################################################################################
#################################################################################


# grr, ENTRYPOINT resets CMD now
ENTRYPOINT ["/apply-security_entrypoint-launcher.sh"]
CMD ["php-fpm"]
