FROM silintl/php-web:latest

RUN apt-get update -y && \
    apt-get install -y php5-ldap

COPY vhost.conf /etc/apache2/sites-enabled/

COPY phpldapadmin-1.2.3/ /data/

EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]
