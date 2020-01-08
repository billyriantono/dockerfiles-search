FROM httpd:2.4

COPY httpd.conf /usr/local/apache2/conf/httpd.conf

RUN apt-get update && apt-get install -y \
    apache2 \
    libapache2-mod-fcgid

#RUN a2enmod rewrite

VOLUME /var/www/html
VOLUME /etc/apache2/sites-enabled