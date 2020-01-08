FROM hzhang/centos-ssh
MAINTAINER "Huan Zhang" <huan_zh@yahoo.com>

ADD ./nginx.repo /etc/yum.repos.d/nginx.repo

RUN yum -y install nginx php-fpm
RUN yum -y install python-setuptools
RUN easy_install pip
RUN pip install supervisor

ADD ./start.sh /start.sh
ADD ./supervisord.conf /etc/supervisord.conf

#setup nginx
ADD ./www.conf /etc/nginx/conf.d/www.conf
RUN mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.bak
RUN echo "<?php phpinfo();?>" > /usr/share/nginx/html/index.php

EXPOSE 80 22

CMD ["/bin/bash", "/start.sh"]
