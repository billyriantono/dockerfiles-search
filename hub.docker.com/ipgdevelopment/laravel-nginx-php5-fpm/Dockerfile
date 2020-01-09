FROM ipgdevelopment/nginx-php5fpm-supervisor:latest
MAINTAINER Nathan Henderson <nhenderson@ipg.com>
RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" > /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
 wget mcrypt php5-cli php5-mcrypt curl git
 
# Laravel requirements
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer
RUN php5enmod mcrypt

# Install composer
RUN bash -c "wget http://getcomposer.org/composer.phar && chmod +x composer.phar && mv composer.phar /usr/local/bin/composer"

# Install PHPUnit
RUN bash -c "wget https://phar.phpunit.de/phpunit.phar && chmod +x phpunit.phar && mv phpunit.phar /usr/local/bin/phpunit"

RUN mkdir /var/www/vhosts && chown www-data:www-data /var/www/vhosts

# Pull Laravel project from github
RUN git clone https://github.com/laravel/laravel.git /var/www/vhosts/laravel/

RUN composer --working-dir=/var/www/vhosts/laravel install --prefer-dist

RUN chown -R www-data:www-data /var/www/vhosts/laravel
RUN chmod -R 775 /var/www/vhosts/laravel/app/storage

# Clean up
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD ./nginx-site.conf /etc/nginx/sites-enabled/default

# Initialization and Startup Script
ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

# private expose
EXPOSE 80

CMD ["/bin/bash", "/start.sh"]
