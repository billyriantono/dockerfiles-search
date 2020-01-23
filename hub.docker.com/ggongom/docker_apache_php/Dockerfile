FROM debian:jessie
MAINTAINER GG
RUN apt-get update && apt-get -y upgrade && apt-get -y install apache2 php5 libapache2-mod-php5 php5-mysql php5-gd && a2enmod headers rewrite ssl && a2dismod status && ln -sf /dev/stderr /var/log/apache2/error.log && ln -sf /dev/stdout /var/log/apache2/access.log
ENTRYPOINT ["/usr/sbin/apachectl","-D","FOREGROUND"]
EXPOSE 80 443
