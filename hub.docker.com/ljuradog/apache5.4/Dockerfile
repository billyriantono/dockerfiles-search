FROM php:5.4-apache
RUN apt-get update
RUN apt-get install -y vim

RUN service apache2 restart
COPY php.ini /usr/local/etc/php/
COPY virtualhost.conf /etc/apache2/sites-enabled/virtualhost.conf
#ENTRYPOINT ["/usr/sbin/apache2ctl"]

EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
