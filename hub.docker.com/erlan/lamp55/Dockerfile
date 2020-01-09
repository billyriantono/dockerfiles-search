FROM ubuntu:14.04
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y apache2 supervisor libapache2-mod-php5 mysql-server php5-mysql php5-gd && rm -rf /var/lib/mysql

ADD ./conf/mysql/my.cnf /etc/mysql/conf.d/my.cnf
ADD ./conf/php/php.ini /etc/php5/apache2/php.ini

ADD ./scripts/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

ADD ./scripts/start.sh /
CMD [ "/start.sh" ]

RUN a2enmod rewrite

CMD ["/usr/bin/supervisord"]
