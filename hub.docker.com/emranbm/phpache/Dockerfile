FROM ubuntu:16.04
RUN apt-get update; apt-get install apache2 php php7.0-fpm php7.0-mysql libapache2-mod-php vim -y; apt-get autoremove
CMD /usr/sbin/apache2ctl -D FOREGROUND
