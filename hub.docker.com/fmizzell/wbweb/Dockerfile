FROM ubuntu:16.04
RUN apt-get update
RUN apt-get install software-properties-common -y
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install php5.6 -y
RUN apt-get install php5.6-mbstring php5.6-mcrypt php5.6-mysql php5.6-xml php5.6-gd -y
RUN apt-get install php-pear php5.6-dev php5.6-mcrypt -y
RUN pecl install xhprof-0.9.4
RUN sed -i -e "\$aextension=xhprof.so" /etc/php/5.6/apache2/php.ini
RUN a2enmod rewrite
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

