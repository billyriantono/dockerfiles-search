FROM identicum/centos-apache:latest
MAINTAINER Gustavo J Gallardo <ggallard@identicum.com>

RUN yum -y install unzip

RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    yum -y install yum-utils && \
    yum-config-manager --enable remi-php72 && \
    yum -y install php

RUN echo "date.timezone = America/Argentina/Buenos_Aires" >> /etc/php.ini
RUN echo "error_log = /proc/1/fd/1" >> /etc/php.ini

RUN cd /var/www && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"
