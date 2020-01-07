FROM ubuntu:12.04

RUN apt-get -y install apache2
RUN apt-get -y install php5-common libapache2-mod-php5 php5-cli


ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80
#ADD html /var/www
ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND"]
