FROM centos:6.6
MAINTAINER Nicolas FATREZ / DIREXI <nfatrez@direxi.com>

COPY mariadb.repo /etc/yum.repos.d/
RUN yum repolist

ENV APP_ENV development

RUN yum -y install MariaDB-server; yum clean all;

COPY conf/my.cnf /etc/

EXPOSE 3306

VOLUME /backup

#ENTRYPOINT ["tail","-f","/var/log/mysql.log"]
COPY run.sh /

CMD /bin/sh /run.sh
