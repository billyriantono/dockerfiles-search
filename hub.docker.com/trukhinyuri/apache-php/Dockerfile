# Version: 0.0.1
FROM ubuntu:14.04
MAINTAINER trukhinyuri <yuri@trukhin.com>
ENV REFRESHED_AT 2014–11–03-1
RUN apt-key update
RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install php5 php5-mysql libapache2-mod-php5 mysql-client wget
RUN apt-get clean
RUN echo "<?php phpinfo(); ?>" >> /var/www/html/info.php
EXPOSE 80
EXPOSE 443
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
