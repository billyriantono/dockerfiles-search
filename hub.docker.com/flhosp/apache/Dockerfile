FROM centos:6
MAINTAINER Kevin Finley <kevishie@gmail.com>

RUN sed -i 's/enabled=1/enabled=0/g' /etc/yum/pluginconf.d/fastestmirror.conf
RUN yum --setopt=tsflags=nodocs -y update
RUN yum --setopt=tsflags=nodocs -y install httpd vim mod_ssl wget unzip && yum clean all

ENV APACHE_LOG_DIR /var/log/httpd

RUN mkdir -p $APACHE_LOG_DIR
RUN chown -R root:root /var/www/html

WORKDIR /var/www/html

EXPOSE 80

CMD ["httpd", "-D", "FOREGROUND"]
