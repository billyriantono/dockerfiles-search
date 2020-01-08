# Debian
FROM php:fpm 
MAINTAINER JimyRyan

#################################################################################
#################################################################################
#                                                                               #
#                [START :: TIMEZONE, LOCALE & UPDATE / UPGRADE]                 #
#                                                                               #
#################################################################################
RUN set -e \
	&& apt-get update -y \
    && apt-get install -y locales

# Set locale and timezone 
ENV LANGUAGE=fr_FR.UTF-8
ENV LANG=fr_FR.UTF-8
ENV LC_ALL=fr_FR.UTF-8
ENV TZ=Europe/Paris

# Change locale and timezone 
RUN set -e \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# '$LANG' UTF-8/'$LANG' UTF-8/' /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=$LANG \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone

# Update distribution
RUN apt-get update -y \
    && apt-get upgrade -y
#################################################################################
#                                                                               #
#                   [END :: TIMEZONE, LOCALE & UPDATE / UPGRADE]                #
#                                                                               #
#################################################################################
#################################################################################

# install the PHP extensions we need
RUN set -e \
    && buildDeps=" \
		# For png-dir
		
		libpng12-dev \
		# For jpeg-dir
		
		libjpeg-dev \
		# For mcrypt
		
		libmcrypt-dev \	
		# For Tidy
		
        libtidy-dev \
		
		libpq-dev \
	"; \
	
	buildExt=" \
		gd \
		mcrypt \
        mbstring \
		opcache \
		pdo \
		pdo_mysql \
		pdo_pgsql \
		zip \
        tidy \
    "; \
	apt-get install -y $buildDeps --no-install-recommends \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install -j$(nproc) $buildExt

# Waiter
ENV DOCKERIZE_VERSION 0.1.0
ENV DOCKERIZE_TIMEOUT 1800
ENV DOCKERIZE_WAIT_SERVICES=
RUN set -xe \
	&& apt-get install -y wget \
	&& wget "https://github.com/jwilder/dockerize/releases/download/v${DOCKERIZE_VERSION}/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz" -O /tmp/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz \
	&& tar -C /usr/local/bin -xzvf /tmp/dockerize-linux-amd64-v${DOCKERIZE_VERSION}.tar.gz	
	
# Remove the apt list
RUN rm -rf /var/lib/apt/lists/* 	
	
# Copy and set default PHP settings
COPY conf/php/*.ini $PHP_INI_DIR/conf.d/
RUN set -e \
	&& chmod 644 $PHP_INI_DIR/conf.d/*

RUN mkdir -p /usr/local/etc/nginx/conf.d/
COPY conf/nginx/*.conf /usr/local/etc/nginx/conf.d
	
# log folder
VOLUME /var/log/php

# PHP settings
ENV PHP_MEMORY_LIMIT 256M
ENV PHP_MAX_EXECUTION_TIME 3600
ENV PHP_UPLOAD_MAX_FILESIZE 100M
ENV PHP_POST_MAX_SIZE 100M
ENV PHP_DISPLAY_ERRORS Off

# Possibility to call the Docker Cloud trigger API for reload in
ENV CALL_API_URL_TRIGGER_WHEN_READY=

# Entrypoint & environement variable
COPY /*.sh /
RUN set -e \
	&& chmod 700 /*.sh

ENTRYPOINT ["/my-entrypoint.sh"]

CMD ["php-fpm"]