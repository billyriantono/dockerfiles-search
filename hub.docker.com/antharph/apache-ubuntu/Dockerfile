
FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

## preesed tzdata, update package index, upgrade packages and install needed software
RUN echo "tzdata tzdata/Areas select Asia" > /tmp/preseed.txt; \
    echo "tzdata tzdata/Zones/Asia select Taipei" >> /tmp/preseed.txt; \
    debconf-set-selections /tmp/preseed.txt && \
    apt-get update && \
    apt-get install -y tzdata apt-utils

RUN apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:ondrej/php
RUN apt-get update \
    && apt-get install -y php5.6 \
    && apt-get install -y php7.0 \
    && apt-get install -y php7.2 \
    && apt-get install apache2 \
    && apt-get install -y vim \
    && apt-get install -y mysql-client htop mytop \
    && echo "ServerName localhost" > /etc/apache2/conf-available/servername.conf \
    && a2enconf servername 

#laravel requirements
RUN apt-get install -y php-gd php-xml php5.6-mbstring php7.0-mbstring php7.2-mbstring \
    php5.6-dom php7.0-dom php7.2-dom php7.0-mcrypt php7.0-curl curl php7.2-bcmath

#set cli php and apache version
RUN update-alternatives --set php /usr/bin/php7.0 \
    && a2dismod php5.6 \
    && a2enmod php7.0

#install composer
RUN apt-get install -y curl php-cli php-mbstring git unzip
RUN cd ~ \
    && curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer

#install mysql drivers
RUN apt-get install -y php5.6-mysql php7.0-mysql php7.2-mysql

# cleanup of files from setup
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN a2enmod rewrite

EXPOSE 80 443

ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
# CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

#lsb_release -a
#ubuntu 18
#https://stackoverflow.com/questions/8671308/non-interactive-method-for-dpkg-reconfigure-tzdata
#https://vitux.com/how-to-install-php5-and-php7-on-ubuntu-18-04-lts/
#https://en.wikipedia.org/wiki/PHP
# https://github.com/docker-library/httpd/blob/17166574dea6a8c574443fc3a06bdb5a8bc97743/2.4/httpd-foreground

# cd /etc/apache2
# ls -l mods-*/*php*
# sudo update-alternatives --config php
# sudo a2dismod php5.6
# sudo a2enmod php7.2
# sudo service apache2 restart
# sudo update-alternatives --config php
