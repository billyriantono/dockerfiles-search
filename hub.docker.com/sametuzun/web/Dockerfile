FROM ubuntu:latest

RUN apt-get update
RUN apt-get -y install apache2 libapache2-mod-php php-mysql wget

RUN wget -O /tmp/wp.tar.gz https://wordpress.org/latest.tar.gz

RUN tar zxvpf /tmp/wp.tar.gz

RUN rm -f /var/www/html/index.html
RUN cp -rv wordpress/* /var/www/html/
RUN rm -rf wordpress /tmp/wp.tar.gz

COPY wp-config.php /var/www/html/wp-config.php

COPY start.sh /start.sh

EXPOSE 80

CMD ["/start.sh"]
