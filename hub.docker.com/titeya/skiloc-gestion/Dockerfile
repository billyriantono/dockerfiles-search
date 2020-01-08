FROM php:5.6-apache-stretch
MAINTAINER Nicolas Bellamy <n.bellamy@titeya.com>

# Surpress Upstart errors/warning
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
apt-get upgrade -y && \
apt-get -y install libmcrypt-dev wget libpng-dev cron && \
apt-get autoremove -y && \
apt-get clean && \
apt-get autoclean

RUN cd /tmp && \
wget https://pear.php.net/install-pear-nozlib.phar && \
php ./install-pear-nozlib.phar && \
pear install Mail Mail_Mime Net_SMTP

RUN a2enmod rewrite

RUN docker-php-ext-install mysql mysqli mcrypt session gd
