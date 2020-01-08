FROM ubuntu:xenial
MAINTAINER Alejandro Suarez <naxvan@naxvan.es>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -y
RUN apt-get install -y curl
RUN apt-get install -y apache2
RUN apt-get install -y libapache2-mod-php
RUN apt-get install -y php-mysql
RUN apt-get install -y php-gd
RUN apt-get install -y php-mbstring
RUN apt-get install -y mysql-server
RUN apt-get clean -y && apt-get autoclean -y
RUN curl -O https://wordpress.org/latest.tar.gz
RUN tar xzvf latest.tar.gz
RUN rm -R /var/www/html/index.html
RUN mv wordpress/* /var/www/html/
RUN chown -R www-data:www-data /var/www/
ADD run.sh /run.sh
RUN chmod 755 /run.sh
RUN service apache2 start
RUN service mysql start

EXPOSE 80

CMD ["/bin/bash","/run.sh"]
