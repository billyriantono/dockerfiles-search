FROM ubuntu
RUN apt-get update
RUN apt-get install apache2 -y
copy index.html /var/www/html/index.html
EXPOSE 80
CMD apachectl -f /etc/apache2/apache2.conf -e info -DFOREGROUND
