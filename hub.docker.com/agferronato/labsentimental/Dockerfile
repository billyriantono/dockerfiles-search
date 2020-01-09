FROM ubuntu:17.10
# MAINTAINER David Amom <davidamom@gmail.com> (deprecated)
LABEL maintainer = "David Amom <davidamom@gmail.com>"
RUN apt-get update -y && apt-get install -y \
    # Apache/2.4.27 (Ubuntu)
    apache2 \
    apache2-utils \
    # PHP 7.1.11-0ubuntu0.17.10.1 (cli) (built: Nov  1 2017 16:30:52) ( NTS )
        php \
        libapache2-mod-php \
        php-common \
        php-mbstring \
        php-xmlrpc \
        php-soap \
        php-gd \
        php-xml \
        php-intl \
        php-mysqlnd \
        php-pgsql \
        php-cli \
        php-mcrypt \
        php-ldap \
        php-zip \
        php-curl \
    # Optional
    #dialog apt-utils \
    nano --fix-missing \
    #curl \

    # Cleaning...
    && apt-get clean && apt-get autoclean && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*
# Setting environment variables
# ENV APACHE_RUN_USER  = "www-data"
# ENV APACHE_RUN_GROUP = "www-data"
# ENV APACHE_LOG_DIR   = "/var/log/apache2"
# ENV APACHE_LOCK_DIR  = "/var/lock"
# ENV APACHE_PID_FILE  = "/var/run/apache2/apache2.pid"

VOLUME /var/www/html
ADD . /application/

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY run /usr/local/bin/run
RUN chmod +x /var/www
RUN chmod +x /usr/local/bin/run
#RUN chown -R www-data:www-data /var/www/html
# Enables apache rewrite module
RUN a2enmod php7.1
RUN a2enmod rewrite
# RUN service apache2 start
#RUN a2enmod rewrite

#SSL
#RUN /usr/sbin/a2ensite default-ssl
#RUN /usr/sbin/a2enmod ssl
# https://httpd.apache.org/docs/2.4/mod/prefork.html
#RUN /usr/sbin/a2dismod 'mpm_*' && /usr/sbin/a2enmod mpm_prefork

LABEL Description=" Apache 2.4.27 Webserver - PHP 7.1.11"
EXPOSE 80
#SSL
#EXPOSE 443

CMD ["/usr/local/bin/run"]