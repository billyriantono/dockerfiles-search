FROM nginx:1.13.6
MAINTAINER Gary Leong <gwleong@gmail.com>

RUN apt-get update -y && apt-get install wget iptables xtables-addons-common libtext-csv-xs-perl -y

ADD install_geolocat.sh /var/tmp/
#RUN /var/tmp/install_geolocat.sh

RUN rm -rf /etc/nginx/sites-enabled/*
