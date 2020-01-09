FROM ubuntu:latest
ENV DEBIAN_FRONTEND noninteractive
# Install basics
RUN apt-get update && apt-get install -y software-properties-common curl nano vim-tiny && \
    add-apt-repository ppa:ondrej/php && rm -rf /var/lib/apt/lists

# Install PHP 5.6
RUN apt-get update && apt-get install -y --allow-unauthenticated php5.6 php5.6-mysql php5.6-mcrypt php5.6-cli php5.6-gd php5.6-curl && rm -rf /var/lib/apt/lists

# Enable apache mods.
RUN a2enmod php5.6
RUN a2enmod rewrite

# Update the PHP.ini file, enable <? ?> tags and quieten logging.
RUN sed -i "s/short_open_tag = Off/short_open_tag = On/" /etc/php/5.6/apache2/php.ini
RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php/5.6/apache2/php.ini

# Manually set up the apache environment variables
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Expose apache.
EXPOSE 80

# Update the default apache site with the config we created.
COPY apache-config.conf /etc/apache2/sites-enabled/000-default.conf
RUN rm -rf /var/www/html/index.html
COPY *.php /var/www/html/

# Install MySQL 5.7
ENV MYSQL_USER=mysql \
    MYSQL_DATA_DIR=/var/lib/mysql \
    MYSQL_RUN_DIR=/run/mysqld \
    MYSQL_LOG_DIR=/var/log/mysql
ENV DB_USER=docker
ENV DB_PASS=docker
ENV DB_NAME=docker

RUN apt-get update && apt-get install -y mysql-server && rm -rf /var/lib/apt/lists
COPY entrypoint.sh /sbin/entrypoint.sh
COPY data.sql /docker-entrypoint-initdb.d/dump.sql
RUN chmod 755 /sbin/entrypoint.sh

# copy checking
COPY checking/* /checking/
RUN chmod +x /checking/*.sh

# copy config
COPY php.ini /etc/php/5.6/cli/php.ini
COPY apache2.conf /etc/apache2/apache2.conf
COPY mysqld.cnf /etc/mysql/mysql.conf.d/mysqld.cnf

#change permission file config
RUN chmod 666 /etc/php/5.6/cli/php.ini
RUN chmod 666 /etc/apache2/apache2.conf
RUN chmod 666 /etc/mysql/mysql.conf.d/mysqld.cnf
RUN chmod 666 /var/www/html/*.php

RUN echo "lpic ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN cat /etc/sudoers
RUN echo 'root:atv' |chpasswd

RUN useradd -ms /bin/bash lpic
RUN echo 'lpic:atv' | chpasswd

RUN chmod 0444 /etc/mysql/mysql.conf.d/mysqld.cnf

# change language to japanese
RUN apt-get update && apt-get install -y language-pack-ja && rm -rf /var/lib/apt/lists
RUN locale-gen ja_JP.UTF-8
RUN echo 'export LANG=ja_JP.UTF-8' >> /home/lpic/.bashrc

WORKDIR /etc/php/5.6/cli

ENTRYPOINT ["/sbin/entrypoint.sh"]