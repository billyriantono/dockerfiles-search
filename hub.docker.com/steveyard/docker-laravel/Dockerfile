# ------------------------------------------------------------------------------
# Docker provisioning script for the docker-laravel web server stack
#
# 	e.g. docker build -t mtmacdonald/docker-laravel:version .
# ------------------------------------------------------------------------------

# ------------------------------------------------------------------------------
# Start with the official Ubuntu 14.04 base image
# ------------------------------------------------------------------------------

FROM ubuntu:14.04

MAINTAINER Steve Yardumian

# Set correct environment variables
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive

# Use Supervisor to run and manage all other services
CMD ["/usr/local/bin/supervisord", "-c", "/etc/supervisord.conf"]

# ------------------------------------------------------------------------------
# Provision the server
# ------------------------------------------------------------------------------

#PATCHED for when mounting a Mac OS X folder in VBox
RUN usermod -u 1000 www-data

RUN mkdir /provision
ADD provision /provision

# Get wget
RUN apt-get update && apt-get -y install wget

# Add source for php5-ldap to apt source list
RUN echo "deb http://security.ubuntu.com/ubuntu trusty-security main" >> /etc/apt/sources.list

# Add postgres source
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" >> /etc/apt/sources.list.d/pgdg.list

# Update
RUN apt-key update && apt-get update

# Install dependencies, beanstalkd task queue (beanstalkd, memchached),
# pdf generation tool (libxrender1)
RUN apt-get -y install curl libcurl3 libcurl3-dev \
                            python \
                            cron \
                            vim \
                            nginx openssl \
                            php5-cli php5-mcrypt php5-pgsql php5-dev php-pear php5-apcu php5-json php5-curl php5-gd php5-gmp php5-imap php5-memcached php5-fpm php5-odbc php5-sybase php5-ldap \
                            postgresql-client-9.4 \
                            git unzip \
                            beanstalkd memcached \
                            libxrender1

# Create nginx ssl dir
RUN mkdir -p /etc/nginx/ssl/

# Install odbc
RUN apt-get -y install unixodbc unixodbc-dev unixodbc-bin libodbc1 \
            odbcinst1debian2 tdsodbc freetds-bin freetds-common freetds-dev \
            libct4 libsybdb5

# Copy over new version of wkhtmltopdf
# Ubuntu ships with an old version so instead copy tool locally
RUN cp /provision/bin/wkhtmltopdf /usr/bin/wkhtmltopdf

# Copy odbc configuration over to container
RUN cp /provision/conf/freetds.conf /etc/freetds/freetds.conf \
    && cp /provision/conf/odbc.ini /etc/odbc.ini \
    && cp /provision/conf/odbcinst.ini /etc/odbcinst.ini

# Put supervisorctl config in place and install supervisorctl
RUN mkdir -p /etc/supervisord/ \
    && mkdir /var/log/supervisord \
    && cp /provision/conf/supervisor.conf /etc/supervisord.conf \
    && cp /provision/service/* /etc/supervisord/ \
    && curl https://bootstrap.pypa.io/ez_setup.py -o - | python \
    && easy_install supervisor

# Configure NginX and disable 'daemonize' in nginx (because we use supervisor instead)
RUN cp /provision/conf/nginx-qa /etc/nginx/sites-available/default \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

# Configure PHP5, enable mcrypt, disable 'daemonize' in php5-fpm (supervisor is used)
RUN cp /provision/conf/php.fpm.ini /etc/php5/fpm/php.ini \
    && cp /provision/conf/php.cli.ini /etc/php5/cli/php.ini \
    && php5enmod mcrypt \
    && sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf

# Install Node and NPM
RUN curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash - \
    && apt-get install -y nodejs

# Install Composer PHP dependency manager
RUN php -r "readfile('https://getcomposer.org/installer');" | php \
    && mv composer.phar /usr/local/bin/composer

# Install bower and gulp
RUN npm install -g bower && npm install -g gulp

# Start nginx and php5-fpm
RUN supervisorctl start nginx && supervisorctl restart php5-fpm

#www-data user must own the cache locations in order to read/write
RUN mkdir -p /var/www/html/
#RUN chown -R www-data /var/www/html/storage
#RUN chown -R www-data /var/www/html/bootstrap/cache

# Install PhantomJS (headless browser)
RUN mkdir /tmp/phantomjs \
    && curl -L -o /tmp/phantomjs.tar.bz2 https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-1.9.8-linux-x86_64.tar.bz2 \
    && tar xvfj /tmp/phantomjs.tar.bz2 -C /tmp/phantomjs --strip 1 \
    && cp /tmp/phantomjs/bin/phantomjs /usr/bin/phantomjs \
    && chmod +x /usr/bin/phantomjs

# Install and enable XDEBUG
RUN apt-get -y install php5-xdebug \
    && cp /provision/conf/xdebug.ini /etc/php5/mods-available/xdebug.ini

# Copy an install script for Selenium server PhantomJS (test tool)
# This is no longer installed by default because it requires the JRE and is large
RUN cp /provision/bin/selenium-setup.sh /home/selenium-setup.sh

RUN mkdir -p /var/www/.aws

# Clean up
RUN rm -rf /provision

# ------------------------------------------------------------------------------
# Prepare image for use
# ------------------------------------------------------------------------------

# Expose ports
EXPOSE 22 80 443

# ------------------------------------------------------------------------------
# Set locale (support UTF-8 in the container terminal)
# ------------------------------------------------------------------------------

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# ------------------------------------------------------------------------------
# Clean up
# ------------------------------------------------------------------------------

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
