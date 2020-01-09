FROM debian:jessie-slim

MAINTAINER Marc Cizeron <marc@cizeron.me>

ARG PROJECT_DIR_ARG='/var/www/app'
ENV PROJECT_DIR=$PROJECT_DIR_ARG

# Add the PPA for PHP 5.6
RUN  apt-get -qq update && apt-get -qqy upgrade && apt-get install -y --force-yes\
  php5 php5-cli php5-mysql php5-mcrypt php5-curl php5-gd php5-intl php5-readline php5-xdebug php5-geos libgeos-dev\
  apache2 libapache2-mod-php5 mariadb-client xvfb sudo curl git-core openssh-client ssh-client less\
  libgeos-dev wget apt-transport-https lsb-release ca-certificates fontconfig fontconfig-config xfonts-75dpi libxrender1

# Update php settings
#COPY php.ini /etc/php/5.6/apache2/php.ini
#COPY php.ini /etc/php/5.6/cli/php.ini
COPY php.ini /etc/php5/apache2/php.ini
COPY php.ini /etc/php5/cli/php.ini

# Enable xdebug
#COPY xdebug.ini /etc/php/5.6/mods-available/xdebug.ini
COPY xdebug.ini /etc/php5/mods-available/xdebug.ini

# Install WP Cli
RUN curl -o /bin/wp-cli.phar https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    printf '#!/bin/sh \n# This is a wrapper so that wp-cli can run as the www-data user so that permissions \n# remain correct \nsudo -E -u www-data /bin/wp-cli.phar "$@"' > /bin/wp && \
    chmod +x /bin/wp-cli.phar /bin/wp && \
    php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer && \
    curl -sL https://deb.nodesource.com/setup_11.x | sudo bash - && \
    apt-get install nodejs && \
    mv /usr/bin/npm /usr/bin/orig-npm && \
    printf '#!/bin/sh \n# This is a wrapper so that npm can run as the www-data user so that permissions# remain correct \nsudo -u www-data /usr/bin/orig-npm "$@"' > /usr/bin/npm && \
    chmod +x /usr/bin/npm && \
    curl -L -o wkhtmltopdf.deb https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.jessie_amd64.deb && \
    dpkg -i wkhtmltopdf.deb && \
    apt-get install -f && \
    # Clear cache
    apt-get clean &&  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    chown www-data:www-data /var/www/ && \
    mkdir -p $PROJECT_DIR && \
    chown www-data:www-data -R $PROJECT_DIR

COPY vhost.conf /etc/apache2/sites-available/app.viaterroirs.dev.conf
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
    a2ensite app.viaterroirs.dev && \
    a2dissite 000-default.conf && \
    a2enmod rewrite && \
    service apache2 restart

ENV APACHE_RUN_USER    www-data
ENV APACHE_RUN_GROUP   www-data
ENV APACHE_PID_FILE    /var/run/apache2.pid
ENV APACHE_RUN_DIR     /var/run/apache2
ENV APACHE_LOCK_DIR    /var/lock/apache2
ENV APACHE_LOG_DIR     /var/log/apache2

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

EXPOSE 80

WORKDIR $PROJECT_DIR
VOLUME $PROJECT_DIR

ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2", "-D", "FOREGROUND"]
