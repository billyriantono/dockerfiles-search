#++++++++++++++++++++++++++++++++++++++
# stratech/apache2.4-php5.6
#++++++++++++++++++++++++++++++++++++++
# Apache 2.4 PHP 5.6  
#++++++++++++++++++++++++++++++++++++++

FROM stratech/ubuntu:14.04
MAINTAINER Stefano Mazzega <stefano.mazzega@gmail.com>

CMD ["/sbin/my_init"]

# Some Environment Variables
ENV    DEBIAN_FRONTEND noninteractive

# Ensure UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

RUN locale-gen en_US.UTF-8

RUN apt-get update
RUN add-apt-repository -y ppa:ondrej/php
RUN apt-get -y --force-yes update && apt-get -y --force-yes install \
						wget  \
						sqlite3  \
						curl  \
						imagemagick \
					 	apache2 \
						libapache2-mod-php5 \
						php5.6 \
						php5.6-cli \
						php5.6-dev \
						php5.6-cgi \
						php5.6-curl \
						php5.6-gd \
						php5.6-mysql \
						php5.6-mbstring \
						php5.6-mcrypt \
						php-memcache \
						php-memcached \
						php-mongo \
						php5.6-json \
						php5.6-pgsql \
						php5.6-sqlite3 \
						php5.6-tidy \
						php-pear

RUN apt-get -y --force-yes update
RUN apt-get -y --force-yes install phpmyadmin

# node js
RUN apt-get -y install npm \
	nodejs-legacy
RUN npm install -g grunt-cli bower gulp

# mongo db
#RUN pecl install mongodb
RUN echo "extension=mongodb.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`

# Apache + PHP requires preforking Apache for best results & enable Apache SSL
# forward request and error logs to docker log collector
RUN a2dismod mpm_event
RUN a2enmod mpm_prefork \
			rewrite \
			alias

# install composer
RUN cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# install java
RUN add-apt-repository -y ppa:webupd8team/java && apt-get update -y
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install -y oracle-java8-installer 

# Apache Default Env
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
RUN ln -sf /dev/stdout /var/log/apache2/access.log
RUN ln -sf /dev/stderr /var/log/apache2/error.log
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

RUN mkdir /var/www/public_html && chown $APACHE_RUN_USER:$APACHE_RUN_GROUP /var/www/public_html 

COPY etc/apache2/sites-enabled/vhost-default.conf /etc/apache2/sites-available/000-default.conf
RUN a2ensite 000-default.conf

# enable phpmyadmin
RUN echo "Include /etc/phpmyadmin/apache.conf" >> /etc/apache2/apache2.conf
COPY usr/share/phpmyadmin/config.inc.php /usr/share/phpmyadmin/config.inc.php

RUN mkdir -p /etc/service/apache2
ADD start.sh /etc/service/apache2/run
RUN chmod +x /etc/service/apache2/run

EXPOSE 80
EXPOSE 22

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*