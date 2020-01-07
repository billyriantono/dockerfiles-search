#Version: 1.00
FROM library/debian
MAINTAINER Klauss Reyes Granados "kreyes@gm.es"
RUN apt-get update && apt-get install -y apache2
ADD index.html /var/www/html/index.html
RUN /etc/init.d/apache2 start
EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND
