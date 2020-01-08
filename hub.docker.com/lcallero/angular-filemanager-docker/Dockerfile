FROM php:7-apache

WORKDIR /var/www/html/

#installing supervisor
RUN apt-get update && apt-get install -y supervisor

COPY echo.sh /opt/echo.sh
COPY supervisord.conf /etc/supervisord.conf

RUN chmod +x /opt/echo.sh

#filemanager stuff
COPY angular-filemanager/ /var/www/html/
RUN mkdir -p /var/www/files; chmod 777 /var/www/files
VOLUME /var/www/files

CMD ["supervisord", "-c", "/etc/supervisord.conf"]

