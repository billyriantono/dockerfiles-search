FROM debian:jessie

RUN apt-get update && apt-get install -y apache2 libapache2-mod-php5 php5 php5-cli  php5-mcrypt php5-mysql php5-apcu php5-gd php5-imagick php5-curl php5-intl php5-ldap less drush nodejs 


RUN apt-get install -y vim ssmtp
#Ajout ssmpt
ADD ssmtp.conf /etc/ssmtp/ssmtp.conf

RUN usermod -u 1000 www-data
RUN a2enmod rewrite 
