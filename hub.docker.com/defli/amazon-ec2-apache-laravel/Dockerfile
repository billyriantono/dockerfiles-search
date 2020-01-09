FROM ubuntu:12.04

# Install dependencies
RUN apt-get update -y

RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:ondrej/php5

RUN apt-get update -y

RUN apt-get install -y git curl apache2 php5 libapache2-mod-php5 php5-mcrypt php5-mysql php5-common

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer

# Install app
RUN rm -rf /var/www/*
ADD . /var/www/
RUN  cd /var/www/ && [ -f composer.json ] && /usr/bin/composer install || echo "composer.json not found!"
RUN [ -d /var/www/storage ] && chmod -R 777 /var/www/storage || echo "Storage not found"
# Configure apache
# 
RUN a2enmod rewrite
RUN chown -R www-data:www-data /var/www
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
EXPOSE 80

CMD ["/usr/sbin/apache2", "-D",  "FOREGROUND"]
