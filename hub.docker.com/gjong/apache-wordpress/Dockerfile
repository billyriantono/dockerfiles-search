FROM gjong/apache

MAINTAINER Gerben Jongerius <g.jongerius@gmail.com>

RUN alias adduser='useradd' && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y wget unzip
RUN wget https://wordpress.org/latest.zip --output-document=/tmp/wordpress.zip

RUN unzip /tmp/wordpress.zip -d /tmp/

RUN rm -rf /var/www/html/*
RUN cp -r /tmp/wordpress/* /var/www/html/
RUN chown www-data:www-data /var/www/html -R
RUN a2enmod rewrite

ADD ./docker/file_limit.conf /etc/apache2/conf-enabled/file_limit.conf
ADD ./docker/000-default.conf /etc/apache2/sites-enabled/000-default.conf

RUN /etc/init.d/mysql start && mysql -u root -e "create database wordpress"

EXPOSE 80

CMD ["/bin/bash", "/start.sh"]