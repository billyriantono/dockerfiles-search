FROM centos:latest

MAINTAINER Faidev <25056592@qq.com>

RUN yum install -y mariadb mariadb-server && \
yum clean all && \
chgrp -R 0 /var/lib/mysql/ /var/log/mariadb/ /var/run/ && \
chmod -R g+rw /var/lib/mysql/ /var/log/mariadb/ /var/run/ && \
find /var/lib/mysql/ /var/log/mariadb/ /var/run/ -type d -exec chmod g+x {} + && \
curl -o docker-entrypoint.sh https://raw.githubusercontent.com/faidev/dockerfile/master/mariadb/docker-entrypoint.sh && \
chmod +x docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

VOLUME /var/lib/mysql

USER 27

EXPOSE 3306

CMD ["mysqld_safe"]
