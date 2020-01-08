#Base docker file for lifeandshell.com
FROM ubuntu
MAINTAINER "Mattias Hemmingsson" <matte.hemmingsson@gmail.com>



#Install deps
RUn apt-get update
RUN  apt-get -y install nginx
RUN apt-get install php-fpm php-mysql php-cli php-xml -y
RUN apt-get install wget curl -y
#Setup db






#Wordpress
ADD wordpress_https.conf /etc/nginx/nginx.conf
##
## ADDING THE TLS VERSION HERE
##
ADD tls/ /etc/nginx/tls/
RUN chmod +r /etc/nginx/tls/*

ADD php.ini	/etc/php/7.2/fpm/php.ini
ADD php-fpm.conf /etc/php/7.2/fpm/conf.d/www.conf
ADD php-fpm.conf_demon /etc/php/7.2/fpm/php-fpm.conf
RUN echo "top" >>/var/log/php7.0-fpm.log
RUN chown www-data:www-data /var/log/php7.0-fpm.log
WORKDIR /var/www
RUN wget https://wordpress.org/wordpress-4.9.8.tar.gz
RUN tar -zxvf wordpress-4.9.8.tar.gz
#RUN chown nginx:nginx -R wordpress
RUN chown www-data:www-data -R wordpress
RUN chmod 755 -R wordpress
RUN chown www-data:www-data -R /var/www/wordpress/wp-content
RUN chmod 775 -R /var/www/wordpress/wp-content

#Setup Healthx
RUN mkdir /var/www/wordpress/healthz/
RUN echo "<html><head><title>All fine</title></head></html>" > /var/www/wordpress/healthz/index.html
RUN chmod 755 /var/www/wordpress/healthz/index.html
RUN chown www-data:www-data /var/www/wordpress/healthz/


#Setup php
RUN mkdir /var/lib/php/session
RUN chown www-data:www-data /var/lib/php/session
RUN chmod 770 /var/lib/php/session


#Fix nfinx
RUN chown www-data:www-data -R /var/lib/nginx/
RUN chown root:www-data /var/log/nginx
RUN chmod 775 -R /var/log/nginx
RUN mkdir /run/php
RUN chown www-data:www-data /run/php
RUN chmod 771 /run/php

ADD start.sh /
RUN chown www-data /start.sh
RUN chmod 700 /start.sh

USER www-data

CMD  /start.sh
