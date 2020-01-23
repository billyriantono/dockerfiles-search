FROM circleci/php:7.2-apache-node
# Install required extensions.
RUN sudo apt-get update
RUN sudo apt-get upgrade
RUN sudo apt-get install -y --no-install-recommends apt-utils
RUN sudo apt-get install -y mysql-client
RUN sudo apt-get install -y libzip-dev
RUN sudo apt-get install -y libpng-dev
RUN sudo apt-get install -y aptitude
RUN sudo docker-php-ext-install pdo_mysql
RUN sudo docker-php-ext-install bcmath
RUN sudo docker-php-ext-install pcntl
RUN sudo docker-php-ext-install gd
RUN sudo aptitude -y install imagemagick
RUN sudo aptitude -y install libmagickcore-dev
RUN sudo aptitude -y install libmagickwand-dev
# Install drush.
RUN composer self-update
RUN composer global require drush/drush:8.*
# Remove x-debug.
Run sudo rm /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini