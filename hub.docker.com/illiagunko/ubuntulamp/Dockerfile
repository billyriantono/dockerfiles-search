FROM ubuntu:16.04

RUN apt-get update
RUN apt-get install php -y 
RUN apt-get install -y php-pear php-fpm php-dev php-zip php-curl php-xmlrpc php-gd php-mysql php-mbstring php-xml libapache2-mod-php
#RUN apt-get install -y apache2 && systemctl start apache2 && systemctl enable apache2 && service apache2 start
EXPOSE 22 80 8080 443 21 9999
