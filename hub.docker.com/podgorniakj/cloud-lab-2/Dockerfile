FROM ubuntu
LABEL maintainer="podgorniakj@example.com"
RUN apt-get update
RUN apt-get -y install apache2
COPY index.html /var/www/html/
RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf
RUN sed -i 's/*:80>/*:8080>/g' /etc/apache2/sites-enabled/000-default.conf 
RUN service apache2 start

