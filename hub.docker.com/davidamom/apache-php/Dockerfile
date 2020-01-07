FROM ubuntu:14.04
MAINTAINER David Amom <davidamom@gmail.com>

RUN apt-get update && apt-get install -y \
    # Apache 2.4.7
    apache2 \
    # PHP 5.5.9
        php5 \
        php5-common \
        # Optional System Utilities and Libraries
        #libapache2-mod-php \
        php5-cli \
        php5-xdebug \
        phpunit \
        # Optional Security/Encryption Utilities and Libraries
        php5-mcrypt \
        # Optional Data Management Utilities and Libraries
        php5-pgsql \
        php5-mysql \
        php5-sybase \
        php5-apcu \
        php5-json \
        # Optional Graphics Utilities and Libraries
        php5-gd \
        php5-imagick \
        # Optional Web Utilities
        php5-curl \
        php5-ldap \
        php-soap \
    # Optional
    #dialog apt-utils \
    nano \
    # Cleaning...
    && apt-get clean && apt-get autoclean && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*
# Setting environment vars
ENV APACHE_RUN_USER  www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR   /var/log/apache2
ENV APACHE_LOCK_DIR  /var/lock
ENV APACHE_PID_FILE  /var/run/apache2.pid
# Enables apache rewrite module
RUN a2enmod rewrite
RUN /usr/sbin/a2ensite default-ssl
RUN /usr/sbin/a2enmod ssl
# https://httpd.apache.org/docs/2.4/mod/prefork.html
RUN /usr/sbin/a2dismod 'mpm_*' && /usr/sbin/a2enmod mpm_prefork
# Setting permissions so that apcu can create cache directories
RUN chmod -R 775 /var/www/html
LABEL Description=" Apache 2.4.7 Webserver - PHP 5.5.9"

VOLUME /var/www/html
# If just want to test an application already installed in dockerhost
## Use ADD or COPY to copy dockerhost content (files, directory) into the container directory.
## In this case, it will copy all content from this context into the container /var/www/html/ directory.
## It's usefull to create images that will just test an application!
## The Dockerfile and 000-default.conf file (app virtualhost configuration)
##     must be inside the app root folder before running docker build image command.
ADD . /var/www/html/
# Copies virtualhost conf file into the container directory.
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

EXPOSE 80 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
#CMD ["/bin/bash"]
# ENTRYPOINT /bin/bash