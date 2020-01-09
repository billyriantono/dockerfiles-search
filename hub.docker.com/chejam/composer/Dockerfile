FROM composer/composer:base

# stirenno iz tut https://github.com/RobLoach/docker-composer/blob/master/master/Dockerfile
MAINTAINER Aleksandr Batalov <abataloff88@gmail.com>

# Install Composer
RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot && rm -rf /tmp/composer-setup.php

# Display version information
RUN composer --version