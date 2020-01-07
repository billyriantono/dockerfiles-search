FROM library/debian:jessie
MAINTAINER fran@francastro.eu
COPY sources.list /etc/apt/sources.list
RUN apt-get update -qq && apt-get -y install apache2 php5 php5-mysql
COPY info.php /var/www/html/info.php
EXPOSE 80

ENTRYPOINT [ "/usr/sbin/apache2ctl", "-D FOREGROUND", "-X" ]
RUN ln -sf /dev/stdout /var/log/apache2/access.log \
	&& ln -sf /dev/stderr /var/log/apache2/error.log
