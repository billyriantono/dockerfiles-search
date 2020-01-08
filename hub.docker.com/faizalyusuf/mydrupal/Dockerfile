FROM drupal:8-apache

LABEL maintainer "Faizal Yusuf faizalace84@gmail.com"

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt-get update && apt-get install -y unzip git

#Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    mv composer.phar /usr/local/bin/composer && \
    php -r "unlink('composer-setup.php');"

#Install Drupal console and set as global executable
RUN php -r "readfile('https://drupalconsole.com/installer');" > drupal.phar && \
	mv drupal.phar /usr/local/bin/drupal && \
	chmod +x /usr/local/bin/drupal

RUN composer require drupal/console:~1.0 \
	--prefer-dist \
	--optimize-autoloader