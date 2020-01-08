#++++++++++++++++++++++++++++++++++++++
# stratech/apache2-php7.0
#++++++++++++++++++++++++++++++++++++++
# Ubuntu 14.04 Apache2 Docker container   
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

RUN usermod -u 1000 www-data

RUN apt-get update && apt-get -y --force-yes install software-properties-common
RUN add-apt-repository -y ppa:ondrej/php
RUN apt-get -y --force-yes update && apt-get -y --force-yes install \
									wget \
									apache2 \
									sqlite3 \
									curl \
									imagemagick \
									libapache2-mod-php7.0 \
									php7.0 \
									php7.0-cli \
									php7.0-cgi \
									php7.0-dev \
									php7.0-mysql \
									php-imagick \
									php-memcache \
									php-memcached \
									php7.0-gd \
									php7.0-json \
									php7.0-curl \
									php7.0-sqlite3 \
									php7.0-intl \
									php7.0-mcrypt \
									php7.0-xsl \
									php-pear \
									libsasl2-dev \
									libssl-dev \
									libsslcommon2-dev \
									libcurl4-openssl-dev
RUN apt-get -y autoremove
RUN apt-get -y upgrade

# node js
RUN apt-get -y --force-yes install npm 
RUN apt-get -y --force-yes install nodejs-legacy 
RUN npm install -g grunt-cli bower

# mongo db
RUN pecl install mongodb
#RUN echo "extension=mongodb.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`

# install java
RUN add-apt-repository -y ppa:webupd8team/java && apt-get update -y
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install -y oracle-java8-installer 

# enable apache mod
RUN a2enmod headers \
			rewrite

# install composer
RUN cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

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


RUN mkdir -p /etc/service/apache2
ADD start.sh /etc/service/apache2/run
RUN chmod +x /etc/service/apache2/run

EXPOSE 80
EXPOSE 22

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*