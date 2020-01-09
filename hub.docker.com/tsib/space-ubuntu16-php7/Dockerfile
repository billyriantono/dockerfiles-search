FROM ubuntu:xenial
MAINTAINER The Space In Between <dev@thespaceinbetween.co.nz>

# Install base packages
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get update
RUN apt-get -yq install curl
RUN apt-get -yq install apache2
RUN apt-get -yq install php
RUN apt-get -yq install php-mbstring
RUN apt-get -yq install libapache2-mod-php
RUN apt-get -yq install php-mysql
RUN apt-get -yq install mysql-client
RUN apt-get -yq install php-mcrypt
RUN apt-get -yq install php-gd
RUN apt-get -yq install php-common
RUN apt-get -yq install php-curl
RUN apt-get -yq install php-pear
RUN apt-get -yq install php-intl
RUN apt-get -yq install php-zip
RUN apt-get install -y php-xdebug
RUN apt-get install -y sendmail
RUN apt-get install -y php-imagick
RUN apt-get install -y aptitude
RUN aptitude install -y libapache2-mod-proxy-html libxml2-dev
RUN apt-get install -y php-dev
RUN apt-get install -y php-soap
RUN apt-get install -y libcurl4-openssl-dev
RUN apt-get install -y pkg-config libssl-dev libsslcommon2-dev
RUN pecl install mongodb
RUN pecl install zip
RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y geoip-database geoip-database-extra php-geoip
RUN apt-get install -y libapache2-mod-geoip

ENV ALLOW_OVERRIDE **False**

# Add image configuration and scripts
ADD run.sh /run.sh
RUN chmod 755 /*.sh

# Configure /app folder with sample app
RUN mkdir -p /app && rm -fr /var/www/html && ln -s /app /var/www/html

RUN usermod -u 1000 www-data
RUN apt-get update
RUN apt-get install -y sendmail
RUN apt-get install -y vim

# Clean the cache
RUN apt-get clean

RUN a2enmod expires
RUN a2enmod headers
RUN phpenmod mcrypt
RUN a2enmod proxy
RUN a2enmod proxy_http
RUN a2enmod proxy_ajp
RUN a2enmod rewrite
RUN a2enmod deflate
RUN a2enmod headers
RUN a2enmod proxy_balancer
RUN a2enmod proxy_connect
RUN a2enmod proxy_html

# Custom helpers
RUN apt-get install -y mc

# Custom apache config to stop loging static files
COPY apache.conf /etc/apache2/sites-available/000-default.conf

RUN service apache2 restart
ADD hosts.sh /home/hosts.sh


EXPOSE 80
WORKDIR /app
CMD ["/run.sh"]
