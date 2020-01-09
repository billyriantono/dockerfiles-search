FROM ubuntu:trusty
MAINTAINER Daniel Hanold (danny@danielhanold.com)

# Environment configuration
# @see https://github.com/docker/docker/issues/4032#issuecomment-192327844
ARG DEBIAN_FRONTEND=noninteractive

# Base webserver packages.
RUN apt-get update && apt-get install -y \
    # Misc packages
    curl \
    git \
    wget \
    htop \
    mysql-client \
    imagemagick \

    # PHP Packages
    php5 \
    php5-common \
    php5-cli \
    php5-fpm \
    php5-xdebug \
    php5-mysql \
    php5-curl \
    php5-gd \
    php5-intl \
    php-pear \
    php5-imagick \
    php5-imap \
    php5-mcrypt \
    php5-memcache \
    php5-memcached \
    php5-ming \
    php5-ps \
    php5-pspell \
    php5-recode \
    php5-sqlite \
    php5-tidy \
    php5-xmlrpc \
    php5-xsl \
    php-apc \
    php5-apcu

# Install SSMTP and modify configuration to use Mailhog on port 1025.
RUN apt-get update && \
    apt-get install ssmtp && \
    sed -i 's/^mailhub=mail*/mailhub=mailhog:1025/' /etc/ssmtp/ssmtp.conf

# Install composer and make it available globally
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    # Verification disabled for now as it seems to break the build
    # php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

# Install drush
RUN php -r "readfile('https://s3.amazonaws.com/files.drush.org/drush.phar');" > /usr/local/bin/drush && \
    chmod +x /usr/local/bin/drush

# Install Drupal Console
RUN curl https://drupalconsole.com/installer -o /usr/local/bin/drupal && \
    chmod +x /usr/local/bin/drupal

# Copy configs
COPY cli_php.ini /etc/php5/cli/php.ini
COPY fpm_php.ini /etc/php5/fpm/php.ini
# Replace www.conf with sed modifications at a later point
COPY www.conf /etc/php5/fpm/pool.d/www.conf

# Create work dir
RUN mkdir -p /var/www/html && \
    chown -R www-data:www-data /var/www

# Create files directory in order to set permissions
# correctly. We will mount a data-only container
# in this location.
RUN mkdir -p /var/www/html/files && \
    touch /var/www/html/files/dummy.txt && \
    chown -R 1000:33 /var/www/html/files && \
    chmod -R 0770 /var/www/html/files

WORKDIR /var/www/html
VOLUME /var/www/html
EXPOSE 9000

# Run PHP5-FPM in the foreground.
CMD ["/usr/sbin/php5-fpm", "-F"]