#FROM docker-registry-default.rocp.vs.csint.cz/rhscl/centos
FROM docker.io/centos

MAINTAINER Jindřich Káňa <jindrich.kana@gmail.com>
LABEL Vendor="ELOS Technologies s.r.o."

RUN yum install -y --setopt=tsflags=nodocs mariadb-server \
    && yum clean all

ADD https://raw.githubusercontent.com/albereinstein/db/master/setupdb.sh /opt
ADD https://raw.githubusercontent.com/albereinstein/db/master/my.cnf /etc
ADD https://raw.githubusercontent.com/albereinstein/db/master/setupdb.sql /opt

RUN mysql_install_db --user=mysql

RUN bash /opt/setupdb.sh
RUN chown -R mysql: /var/lib/mysql \
    && chmod -R 0777 /var/lib/mysql

ENV albert=einstein

EXPOSE 3306

RUN /usr/bin/cat /etc/my.cnf > /tmp/my.cnf \
    && chmod 0777 /tmp/my.cnf

ENTRYPOINT ["/usr/bin/mysqld_safe", "--datadir=/var/lib/mysql", "--user=mysql"]
