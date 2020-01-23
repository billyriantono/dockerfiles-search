FROM ubuntu:14.04

MAINTAINER Ewall Team <ewallteam@gmail.com>

# Setup environment
ENV DEBIAN_FRONTEND noninteractive

# Update sources
RUN apt-get update -y

# install http
RUN apt-get install -y apache2 vim bash-completion unzip
RUN apt-get install -y git
RUN mkdir -p /var/lock/apache2 /var/run/apache2
ADD 000-default.conf /etc/apache2/sites-available/
RUN sudo a2enmod rewrite

# Install mysql client and server
RUN apt-get -y install mysql-client mysql-server curl

#sendmail
RUN apt-get -y install sendmail
ADD sendmail.sh /home/sendmail.sh

#move magento files to html folder
RUN rm -rf /var/www/html/*
ADD demo /var/www/html/
ADD ./stackmagento.sql /var/www/html/sql/
RUN chmod -Rf 777 /var/www/html
COPY local.xml /var/www/html/app/etc/

# install php
RUN apt-get install -y php5 php5-mysql php5-dev php5-gd php5-memcache php5-pspell php5-snmp snmp php5-xmlrpc libapache2-mod-php5 php5-cli php5-curl php5-mcrypt

# install supervisord
RUN apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor

# install sshd
RUN apt-get install -y openssh-server openssh-client passwd
RUN mkdir -p /var/run/sshd
RUN sed -ri 's/PermitRootLogin without-password/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN echo 'root:root' | chpasswd

# Put your own public key at id_rsa.pub for key-based login.
RUN mkdir -p /root/.ssh && touch /root/.ssh/authorized_keys && chmod 700 /root/.ssh
ADD supervisord.conf /etc/

EXPOSE 22 8080 443
CMD ["supervisord", "-n"]

#run the magento cron
RUN apt-get -y install rsyslog
ADD crontab /etc/crontab
ADD start-cron.sh /usr/bin/start-cron.sh
RUN chmod +x /usr/bin/start-cron.sh
RUN touch /var/log/cron.log

#install the database
RUN /bin/bash -c "/usr/bin/mysqld_safe &" && \
  	sleep 5 && \
 	mysql -u root -e 'CREATE DATABASE `home-full-width-02`' && \
  	mysql -u root -e 'CREATE USER "home-full-02"@"localhost" IDENTIFIED BY "homefull02@123"' && \
  	mysql -u root -e 'GRANT ALL PRIVILEGES ON `home-full-width-02`.* TO "home-full-02"@"localhost" WITH GRANT OPTION' && \
  	mysql -u root home-full-width-02 < /var/www/html/sql/stackmagento.sql && \
  	mysql -u root -e 'exit'
