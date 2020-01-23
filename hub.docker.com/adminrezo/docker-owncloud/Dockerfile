# Owncloud 7 / Debian 7
#
# VERSION 0.3
#

FROM     adminrezo/docker-lamp
MAINTAINER Nico Dewaele "nico@adminrezo.fr"

ENV DEBIAN_FRONTEND noninteractive

# Upgrade & depends

RUN (apt-get update && apt-get upgrade -y -q && apt-get dist-upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)
RUN apt-get update && apt-get install -y -q wget
RUN wget http://download.opensuse.org/repositories/isv:ownCloud:community/Debian_7.0/Release.key
RUN apt-key add Release.key  
RUN echo 'deb http://download.opensuse.org/repositories/isv:/ownCloud:/community/Debian_7.0/ /' >> /etc/apt/sources.list.d/owncloud.list 
RUN apt-get update && apt-get install -y -q owncloud


# Reconf Php5 & Apache

ADD default-ssl /etc/apache2/sites-available/default-ssl
ADD default /etc/apache2/sites-available/default
RUN a2ensite default-ssl
RUN a2dissite default
RUN a2enmod ssl

ADD pre-conf.sh /pre-conf.sh
RUN chmod 750 /pre-conf.sh
RUN (/bin/bash -c /pre-conf.sh)

RUN mkdir /ocdata && chown www-data.www-data -R /ocdata

EXPOSE 443
CMD ["supervisord", "-n"]
