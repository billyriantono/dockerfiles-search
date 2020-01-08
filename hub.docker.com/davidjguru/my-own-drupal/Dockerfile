FROM drupal:8.7.2-apache

MAINTAINER davidjguru <davidjguru@gmail.com>

# Update the OS (based originally in debian:stretch-slim)
RUN apt-get update && apt-get install -yqq \
        curl \
        git \
        mysql-client \
        vim \
        wget

# Install Composer (Latest version) and Prestissimo as extension to speed up Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
	php composer-setup.php && \
	mv composer.phar /usr/local/bin/composer && \
	php -r "unlink('composer-setup.php');" && \
        composer global require "hirak/prestissimo:^0.3"

# Install Drush Global Launcher 
RUN wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/download/0.4.2/drush.phar && \
	chmod +x drush.phar && \
	mv drush.phar /usr/local/bin/drush 

RUN echo "Drupal was downloaded in the Docker Container"
