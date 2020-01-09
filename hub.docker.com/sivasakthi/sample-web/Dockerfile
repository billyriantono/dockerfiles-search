FROM ubuntu

MAINTAINER DEVOPS

RUN apt-get update 
RUN    apt-get install -y apache2

RUN chmod 775 /var/www/html
COPY index.html tiger.jpg /var/www/html/

EXPOSE  80
CMD ["/etc/init.d/apache2 start"]
