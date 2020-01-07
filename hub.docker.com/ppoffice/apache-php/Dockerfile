FROM ubuntu:trusty
MAINTAINER PPOffice <ppoffice_2008@163.com>

# Install applications
RUN apt-get update && apt-get -y install apache2 php5 && apt-get -y autoremove && apt-get clean

RUN /usr/sbin/a2enmod rewrite

ADD 000-default.conf /etc/apache2/sites-available/

# Site's root directory
VOLUME ["/var/www"]

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]