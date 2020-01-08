FROM fedora/ssh

MAINTAINER Yohan Graterol <yohangraterol92@gmail.com>

VOLUME ["/app"]

RUN yum update -y

RUN yum install redhat-rpm-config -y

RUN yum install freetype-devel libjpeg-devel libpng-devel -y

RUN yum groupinstall -y "Development Tools"

RUN yum install -y python-devel python-virtualenv supervisor mariadb-libs mariadb-devel postgresql-devel postgresql-libs sqlite python-pip GeoIP GeoIP-update GeoIP-devel python-pygeoip

RUN yum install -y libffi-devel libcurl-devel wget tar

RUN yum install npm

RUN yum clean all

RUN wget http://www.maxmind.com/download/geoip/api/c/GeoIP.tar.gz

RUN tar xvf GeoIP.tar.gz

RUN cd GeoIP-1.4.8/;./configure;make;make install

RUN rm -rf GeoIP*

EXPOSE 8000

