FROM phpdockerio/php73-fpm:latest

# Set on-build env values
ARG buildtime_workdir="/var/www/html"
ENV APP_WORKDIR=${buildtime_workdir}

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install php7.3-mysql php7.3-gd php-imagick php7.3-imap php7.3-intl php-mongodb php-ssh2 php-yaml \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

CMD alias composer='/usr/local/bin/composer'

# Set working directory
WORKDIR ${APP_WORKDIR}

# Open port
EXPOSE 9000
