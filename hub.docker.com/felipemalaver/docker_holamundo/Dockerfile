FROM eboraas/apache
MAINTAINER Felipe Malaver

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY index.html /var/www/html/index.html

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]