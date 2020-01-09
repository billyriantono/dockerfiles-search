# Composer Docker Container
# Base Dockerfile: composer/base
FROM kprokopenko/php
MAINTAINER Konstantin Prokopenko <kprokopenko@gmail.com>

RUN echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config

# Environmental Variables
ENV COMPOSER_HOME /composer

# Add global binary directory to path
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

# Setup the Composer installer
ENV COMPOSER_INSTALLER_SHA384 "7228c001f88bee97506740ef0888240bd8a760b046ee16db8f4095c0d8d525f2367663f22a46b48d072c816e7fe19959"
RUN php -r "readfile('https://getcomposer.org/installer');" > /tmp/composer-setup.php \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== '${COMPOSER_INSTALLER_SHA384}') { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"

# Set up the volumes and working directory
VOLUME ["/composer"]

ENV COMPOSER_VERSION master
RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot && rm -rf /tmp/composer-setup.php

# Display version information
RUN composer --version

# Set up the command arguments
CMD ["-"]
ENTRYPOINT ["composer", "--ansi"]
