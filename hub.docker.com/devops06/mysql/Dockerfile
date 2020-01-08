FROM devops06/centos:7

MAINTAINER zhfang@dataman-inc.com

ENV PACKAGE_URL http://repo.mysql.com/yum/mysql-5.6-community/el/7/x86_64/mysql-community-server-5.6.34-2.el7.x86_64.rpm

ADD mysql.repo  /etc/yum.repos.d/mysql.repo

# Install server
RUN yum install -y $PACKAGE_URL \
    && yum clean all \
    && rm -rf /var/cache/yum/*\
    && mkdir /docker-entrypoint-initdb.d

COPY my.cnf.temp /etc/my.cnf
COPY docker-entrypoint.sh /entrypoint.sh
COPY init_mycnf.sh /

RUN chmod +x *.sh

ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld"]
