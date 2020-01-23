FROM php:5.6-apache

RUN DEBIAN_FRONTEND=noninteractive apt-get -y update

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apt-utils software-properties-common mysql-client mlocate nano wget git imagemagick libmcrypt-dev ncftp cron sudo libfreetype6-dev libjpeg62-turbo-dev libpng12-dev libgtk-3* abiword abiword-* zip zlib1g-dev gawk

RUN docker-php-ext-install pdo pdo_mysql mysqli mcrypt -j$(nproc) iconv mcrypt && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && docker-php-ext-install -j$(nproc) gd && docker-php-ext-install zip

RUN apt-get install -y --no-install-recommends libmagickwand-dev && rm -rf /var/lib/apt/lists/*

RUN pecl install imagick-3.4.1 && docker-php-ext-enable imagick

COPY php.ini /usr/local/etc/php/
COPY 000-default.conf /etc/apache2/sites-available/
COPY security /etc/apache2/conf-available/

COPY yram-init /usr/local/bin/

ADD crontab /etc/cron.d/yram


COPY .bashrc /root/

RUN a2enmod rewrite.load && service apache2 restart

# Make ssh dir
RUN mkdir /var/www/.ssh/

# Copy over private key, and set permissions
ADD id_rsa /var/www/.ssh/id_rsa

RUN chmod 400 /var/www/.ssh/id_rsa

# Create known_hosts
RUN touch /var/www/.ssh/known_hosts

# Add bitbuckets key
RUN ssh-keyscan bitbucket.org >> /var/www/.ssh/known_hosts

# RUN sudo -uwww-data git clone git@bitbucket.org:Rafale-D/yram_app.git /var/www/html

RUN chown -R www-data:www-data /var/www/.ssh

RUN mkdir -p /var/www/sessions

RUN chown -R www-data:www-data /var/www

CMD ["yram-init"]