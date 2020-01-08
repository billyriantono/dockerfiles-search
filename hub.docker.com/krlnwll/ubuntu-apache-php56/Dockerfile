FROM ubuntu:14.04

# disable interactive functions
ENV DEBIAN_FRONTEND noninteractive

#Install 
RUN apt-get update
RUN apt-get install -y apache2 
RUN apt-get install -y php5 php5-mysqlnd openssl curl php5-curl

#Copy config
COPY config/vhost.conf /etc/apache2/sites-available/000-default.conf

RUN chown -R www-data:www-data /var/www/html/ \
    && a2enmod rewrite

RUN rm -rf /var/www/html/*

EXPOSE 80 8080 443 3306 25

CMD /usr/sbin/apache2ctl -D FOREGROUND
