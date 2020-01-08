FROM ubuntu:latest
RUN apt-get update \
  && apt-get install -y \
       apache2 \
       php7.0 \
       libapache2-mod-php7.0 \
       curl

WORKDIR /var/www/html
RUN rm -f index.html
ADD files/index.php .

CMD [ "apachectl", "-d", "/etc/apache2", "-f", "/etc/apache2/apache2.conf", "-e",  "info",  "-D", "FOREGROUND" ]
