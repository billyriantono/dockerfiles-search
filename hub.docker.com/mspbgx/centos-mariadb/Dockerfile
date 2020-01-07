FROM centos:latest

MAINTAINER Maximilian Sparenberg sparenberg@openenv.de

RUN yum -y install --setopt=tsflags=nodocs epel-release && \
    yum -y install --setopt=tsflags=nodocs mariadb-server bind-utils pwgen psmisc hostname && \
    yum -y erase vim-minimal && \
    yum -y update && yum clean all

USER root

COPY docker-entrypoint.sh /

RUN chgrp -R 0 /var/lib/mysql/ /var/log/mariadb/ /var/run/
RUN chmod -R g+rw /var/lib/mysql/ /var/log/mariadb/ /var/run/
RUN find /var/lib/mysql/ -type d -exec chmod g+x {} +
RUN find /var/log/mariadb/ -type d -exec chmod g+x {} +
RUN find /var/run/ -type d -exec chmod g+x {} +


VOLUME /var/lib/mysql

USER 1000

EXPOSE 3306
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["mysqld_safe"]
