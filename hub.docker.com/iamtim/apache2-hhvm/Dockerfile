FROM ubuntu:15.04
MAINTAINER Tim Rose <me@iamtim.de>

VOLUME [ "/var/www" ]

RUN echo "deb http://archive.ubuntu.com/ubuntu vivid main universe" > /etc/apt/sources.list

RUN apt-get update
RUN apt-get dist-upgrade -y

RUN apt-get install -y software-properties-common python-software-properties
RUN apt-get install -y wget nano
RUN apt-get install -y apache2 python-setuptools curl git unzip

# Keep upstart from complaining
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl

# Add HHVM repository
RUN apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449
RUN add-apt-repository "deb http://dl.hhvm.com/ubuntu vivid main"

# Run after setting repositories
RUN apt-get update -y

# Basic Requirements
RUN apt-get install -y hhvm

# Supervisor Install
RUN /usr/bin/easy_install supervisor

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2

RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

ADD ./000-default.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod proxy_fcgi

RUN chown -R www-data:www-data /var/www

ADD ./supervisord.conf /etc/supervisord.conf

# Initialization and Startup Script
ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

# private expose
EXPOSE 80

CMD ["/start.sh"]
