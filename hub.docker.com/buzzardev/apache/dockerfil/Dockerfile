FROM ubuntu:16.04
MAINTAINER Alexey <tankov.aa@yandex.ru>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
#ADD sources.list /etc/apt/sources.list
RUN apt-get -y install apache2 php-fpm
#RUN apt-get -y install libapache2-mod-fastcgi
ADD ports.conf /etc/apache2/ports.conf
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf
#RUN systemctl reload apache2

#RUN a2dismod php7.0
RUN a2enmod actions

ADD fastcgi.conf /etc/apache2/mods-enabled/fastcgi.conf
#RUN systemctl reload apache2

RUN mkdir -v /var/www/go-rost.ru
COPY public/ /var/www/go-rost.ru
# RUN iptables -I INPUT -p tcp --dport 8080 ! -s 192.168.44.46 -j REJECT --reject-with tcp-reset
ADD gorost.conf /etc/apache2/sites-available/gorost.conf

#RUN a2ensite go-rost.ru
#RUN systemctl reload apache2

RUN apt-get install nginx -y
RUN rm /etc/nginx/sites-enabled/default
ADD apache /etc/nginx/sites-available/apache
RUN ln -s /etc/nginx/sites-available/apache /etc/nginx/sites-enabled/apache
#RUN systemctl reload nginx

RUN apt-get install unzip build-essential apache2-dev wget -y
#RUN wget https://github.com/gnif/mod_rpaf/archive/stable.zip
#RUN unzip stable.zip
#RUN cd mod_rpaf-stable && \
#make
#RUN make mod_rpaf -y
#ADD rpaf.conf /etc/apache2/mods-available/rpaf.conf

#RUN a2enmod rpaf
#RUN sudo systemctl reload apache2

# for http (apache, only if ALLOW_INSECURE = true)
EXPOSE 80
# for MySQL server (mariadb, only if START_MYSQL = true)
EXPOSE 3306

#CMD start-servers;
#CMD ["/bin/bash", "-l"]