FROM ubuntu:15.04
MAINTAINER HE201408@students.ephec.be
RUN apt-get update && apt-get upgrade
RUN apt-get install -y apt-utils
RUN apt-get install -y apache2
RUN apt-get install -y php5
RUN apt-get install -y php5-mysql

RUN a2enmod php5
RUN a2enmod rewrite

RUN sed -i "s/short_open_tag = Off/short_open_tag = On/" /etc/php5/apache2/php.ini
RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php5/apache2/php.ini

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

EXPOSE 80

ADD www/www.wt14.ephec-ti.be /var/www/www.wt14.ephec-ti.be
ADD www/intranet.wt14.ephec-ti.be /var/www/intranet.wt14.ephec-ti.be
ADD www/b2b.wt14.ephec-ti.be /var/www/b2b.wt14.ephec-ti.be
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf
CMD ["apache2ctl", "-D", "FOREGROUND"]]
