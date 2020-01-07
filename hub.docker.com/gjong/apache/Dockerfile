FROM ubuntu

MAINTAINER Gerben Jongerius <g.jongerius@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update 
RUN alias adduser='useradd' && DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server apache2 supervisor
RUN apt-get install -y php5 php5-imap php5-mcrypt php5-gd php5-curl php5-mysql php-pear
RUN chown -R www-data:www-data /var/www

ADD ./supervisord.conf /etc/supervisor/conf.d/apache.conf
ADD ./start.sh /start.sh

RUN chmod 755 /start.sh

EXPOSE 80

CMD ["/bin/bash", "/start.sh"]