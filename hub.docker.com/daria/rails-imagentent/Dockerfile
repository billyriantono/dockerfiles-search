FROM php:7.2-apache

RUN DEBIAN_FRONTEND=noninteractive apt-get -y update --fix-missing

RUN rm /etc/apt/preferences.d/no-debian-php

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apt-utils software-properties-common mysql-client mlocate nano wget git imagemagick libmcrypt-dev ncftp cron sudo libfreetype6-dev libjpeg62-turbo-dev libpng-dev libgtk-3* abiword abiword-* zip zlib1g-dev gawk libxml2-dev php-soap wkhtmltopdf --fix-missing

RUN docker-php-ext-install pdo pdo_mysql mysqli -j$(nproc) iconv calendar bcmath && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install -j$(nproc) gd && docker-php-ext-install zip && docker-php-ext-install soap

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends libmagickwand-dev && rm -rf /var/lib/apt/lists/*

RUN pecl install mcrypt-1.0.1 && docker-php-ext-enable mcrypt

RUN pecl install imagick-3.4.3 && docker-php-ext-enable imagick

RUN docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install opcache

RUN curl -sS https://getcomposer.org/installer | php && chmod +x composer.phar && mv composer.phar /usr/local/bin/composer

COPY php.ini /usr/local/etc/php/
COPY opcache.ini /usr/local/etc/php/conf.d/
COPY 000-default.conf /etc/apache2/sites-available/

COPY .bashrc /root/

RUN a2enmod rewrite.load && a2enmod headers.load

COPY security.conf /etc/apache2/conf-available/

RUN service apache2 restart

#OPCACHE DIR
RUN mkdir /var/www/.opcache

# Make ssh dir
RUN mkdir /var/www/.ssh/

# Copy over private key, and set permissions
ADD id_rsa /var/www/.ssh/id_rsa

# Create known_hosts
RUN touch /var/www/.ssh/known_hosts
# Add bitbuckets key
RUN ssh-keyscan gitlab.com >> /var/www/.ssh/known_hosts

RUN chown -R www-data:www-data /var/www/.ssh

RUN mkdir -p /var/www/sessions

RUN chown -R www-data:www-data /var/www
