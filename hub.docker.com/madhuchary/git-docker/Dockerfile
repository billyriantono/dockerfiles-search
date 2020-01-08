FROM ubuntu
RUN apt-get update
RUN apt-get install apache2 -y
COPY index.html /var/www/html/index.html
CMD apachectl -f  /etc/apache2/apache2.conf -e info -DFOREGROUND
