FROM debian:wheezy
MAINTAINER Pavel Bezrukov "bezrukov.ps@gmail.com"

# Get noninteractive frontend for Debian to avoid some problems:
#    debconf: unable to initialize frontend: Dialog
ENV DEBIAN_FRONTEND noninteractive

# Install packages
RUN apt-get update && apt-get -y dist-upgrade && apt-get -y upgrade

# Install program to configure locales
RUN apt-get install -y locales -qq && locale-gen ru_RU.UTF-8 ru_ru && dpkg-reconfigure locales && dpkg-reconfigure locales && locale-gen C.UTF-8 && /usr/sbin/update-locale LANG=C
ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
ENV LC_ALL C.UTF-8

#RUN apt-get install -y locales locale-gen
#RUN dpkg-reconfigure locales && \
#  locale-gen ru_RU.UTF-8 && \
#  /usr/sbin/update-locale LANG=ru_RU.UTF-8
# Install needed default locale for Makefly
#RUN echo 'ru_RU.UTF-8 UTF-8' >> /etc/locale.gen && \
#  locale-gen
# Set default locale for the environment
#ENV LC_ALL ru_RU.UTF-8
#ENV LANG ru_RU.UTF-8
#ENV LANGUAGE ru_RU.UTF-8

# Set the locale
#RUN locale-gen ru_RU.UTF-8..
#ENV LANG ru_RU.UTF-8..
#ENV LANGUAGE ru_RU:ru..
#ENV LC_ALL ru_RU.UTF-8..

#Install base programm & LAMP server
RUN apt-get -y -q install mc vim nano telnet htop wget man sudo pwgen tar unzip curl \
  openssl openssl-blacklist ssl-cert git \
  apache2 apache2-utils libapache2-mod-php5 \
  mysql-server mysql-client phpmyadmin\
  php5-mysql php5-cli php5-common php5-mcrypt php5-gd php5-memcached php5-curl php-pear \
  memcached

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

ADD http://www.1c-bitrix.ru/download/scripts/bitrixsetup.php /var/www/html/
RUN chown -R www-data:www-data /var/www/html && chown -R www-data:www-data /var/lib/php5

EXPOSE 80 3306

# Define default command.
CMD ["/bin/bash"]