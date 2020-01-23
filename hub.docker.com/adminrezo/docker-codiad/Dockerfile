# Codiad, a Web IDE
#
# VERSION               20-03-2015
#

FROM     debian:jessie
MAINTAINER Nicolas Dewaele "nicolas.dewaele@esiee.fr"

ENV DEBIAN_FRONTEND noninteractive


# Installs

RUN echo "deb http://ftp.fr.debian.org/debian/ jessie main non-free contrib" > /etc/apt/sources.list
RUN (apt-get update && apt-get upgrade -y -q && apt-get dist-upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)
RUN apt-get install -y -q supervisor apache2 libapache2-mod-php5 php5 wget unzip pwgen
RUN apt-get -y -q clean


# Codiad install

RUN wget https://github.com/Codiad/Codiad/archive/master.zip
RUN unzip master.zip && rm -f master.zip
RUN mv Codiad-master /var/www/html/codiad

# Codiad Terminal install

RUN wget https://github.com/Fluidbyte/Codiad-Terminal/archive/master.zip
RUN unzip master.zip && rm -f master.zip
RUN mv Codiad-Terminal-master /var/www/html/codiad/plugins/terminal
RUN pwd=$(pwgen 8 1)
RUN echo $pwd && sleep 10
RUN sed -i "s/'PASSWORD','terminal'/'PASSWORD','$pwd'/g" /var/www/html/codiad/plugins/terminal/emulator/term.php


# Apache setup

RUN chown -R www-data.www-data /var/www
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf
ADD default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
RUN a2enmod ssl
RUN a2ensite default-ssl

ADD supervisor-apache.conf /etc/supervisor/conf.d/supervisor-apache.conf
EXPOSE 443
ADD start.sh /start.sh
CMD /start.sh
