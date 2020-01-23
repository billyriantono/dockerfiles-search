FROM php:7.0-fpm
MAINTAINER themoroccan09 <themoroccan@github>


# Install utilities
RUN apt-get update \
        && apt-get install -y \
                zip \
                unzip \
                wget \
                curl \
                git \
                nano \
                openssl \
                cron \
                supervisor \
                htop \
        && rm -rf /var/lib/apt/lists/*

# gd
RUN buildRequirements="libpng-dev libjpeg-dev libfreetype6-dev" \
        && apt-get update && apt-get install -y ${buildRequirements} \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/lib \
        && docker-php-ext-install gd \
        && apt-get purge -y ${buildRequirements} \
        && rm -rf /var/lib/apt/lists/*

# pdo_mysql
RUN docker-php-ext-install pdo_mysql

# mysqli
RUN docker-php-ext-install mysqli

# mcrypt
RUN runtimeRequirements="re2c libmcrypt-dev" \
        && apt-get update && apt-get install -y ${runtimeRequirements} \
        && docker-php-ext-install mcrypt \
        && rm -rf /var/lib/apt/lists/*

# mbstring
RUN docker-php-ext-install mbstring

# zip
RUN buildRequirements="zlib1g-dev" \
        && apt-get update && apt-get install -y ${buildRequirements} \
        && docker-php-ext-install zip \
        && apt-get purge -y ${buildRequirements} \
        && rm -rf /var/lib/apt/lists/*

# xml
RUN 	apt-get update \
	&& apt-get install -y \
	libxml2-dev \
	libxslt-dev \
	&& docker-php-ext-install \
		dom \
		xmlrpc \
		xsl
#Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
	&& php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
	&& php composer-setup.php  \
	&& php -r "unlink('composer-setup.php');" \
	&& mv composer.phar /usr/local/bin/composer


# create symlink to support standard /usr/bin/php
RUN ln -s /usr/local/bin/php /usr/bin/php


#Cron
COPY ./cron-kpi /home
RUN crontab /home/cron-kpi
RUN touch /var/log/cron.log
RUN rm /home/cron-kpi


# Add Costum  php conf
COPY my-configuration.conf /usr/local/etc/php-fpm.d/

# Activate login for user www-data
RUN chsh www-data -s /bin/bash

# Spervisor
COPY laravel-worker.conf /etc/supervisor/conf.d/

#ENTRYPOINT CRON AND PHPFPM
COPY ./entrypoint.sh /

WORKDIR /var/www
EXPOSE 9000
ENTRYPOINT /entrypoint.sh
