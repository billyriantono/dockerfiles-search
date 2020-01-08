FROM fedora:21
MAINTAINER "Christophe Brun" <christophe.brun.cl194@gadz.org>

RUN yum -y update
RUN yum -y install community-mysql-server community-mysql
RUN yum -y install supervisor
RUN yum clean all

EXPOSE 3306

ADD supervisord.conf /etc/supervisord.conf
ADD start.sh /start.sh
ADD config_mysql.sh /config_mysql.sh
RUN chmod 755 /start.sh
RUN chmod 755 /config_mysql.sh
RUN /config_mysql.sh

CMD ["/bin/bash","/start.sh"]

