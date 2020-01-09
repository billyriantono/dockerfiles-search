FROM ubuntu:14.04

RUN apt-get -y update && \
  apt-get -y -q dist-upgrade && \
  apt-get -y install unixodbc unixodbc-dev && \
  # PHP FPM.
  apt-get -y install php5-fpm && \
  # PHP CLI.
  apt-get -y install php5-cli && \
  # PHP extensions.
  apt-get -y install php5-curl && \
  apt-get -y install php5-gd && \
  apt-get -y install php5-imagick && \
  apt-get -y install php5-memcached && \
  apt-get -y install php5-mcrypt && \
  apt-get -y install php5-mongo && \
  apt-get -y install php5-mysql && \
  apt-get -y install php5-oauth && \
  apt-get -y install php5-readline && \
  apt-get -y install php5-redis && \
  apt-get -y install php5-xdebug && \
  apt-get -y install php5-xhprof && \
  apt-get -y install php5-odbc && \
  apt-get -y install php5-mssql && \
  # MySQL client.
  apt-get -y install mysql-client && \
  # Apache.
  apt-get -y install apache2 && \
  a2enmod proxy proxy_fcgi rewrite && \
  #SSH.
  apt-get -y install openssh-server && \
  # Curl.
  apt-get -y install curl && \
  # Composer.
  apt-get -y install git && \
  curl -sS https://getcomposer.org/installer | php5 && \
  mv composer.phar /usr/local/bin/composer && \
  composer global require drush/drush:7.* && \
  ln -s $HOME/.composer/vendor/drush/drush/drush /usr/local/bin/drush && \
  # Python & Supervisord.
  apt-get -y install python-setuptools python-pip && \
  pip install supervisor && \
  # Make www-data user uid/gid 1000 since this is the uid that boot2docker
  # will use for mounted directories.
  usermod -u 1000 www-data && \
  groupmod -g 1000 www-data && \
  drush dl registry_rebuild && \
  cd /tmp && \
    wget ftp://ftp.freetds.org/pub/freetds/stable/freetds-0.95.tar.gz && \
    tar -xvzf freetds-0.95.tar.gz && \
    cd freetds-0.95 && \
    ./configure --prefix=/usr/local && \
    make && \
    make install && \
    cd /tmp && \
    rm -f ftp://ftp.freetds.org/pub/freetds/stable/freetds-0.95.tar.gz && \
    rm -rf freetds-0.95

# For SSH.
ENV NOTVISIBLE "in users profile"
RUN mkdir -p /var/run/sshd && \
  sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
  echo "export VISIBLE=now" >> /etc/profile

# Configuration files.
ADD default /etc/apache2/sites-available/000-default.conf
ADD php.ini /etc/php5/fpm/php.ini
ADD php-cli.ini /etc/php5/cli/php.ini
ADD www.conf /etc/php5/fpm/pool.d/www.conf
ADD entrypoint.sh /entrypoint.sh
ADD cron-entrypoint.sh /cron-entrypoint.sh
ADD supervisord.conf /usr/local/etc/supervisord.conf

# Entry points.
RUN chmod u+x /entrypoint.sh && chmod u+x /cron-entrypoint.sh

ENTRYPOINT /entrypoint.sh

EXPOSE 80
EXPOSE 22
