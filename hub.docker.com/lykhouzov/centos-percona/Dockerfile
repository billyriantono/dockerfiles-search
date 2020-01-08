FROM centos:7
MAINTAINER Aleksandr Lykhouzov <lykhouzov@gmail.com>


# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r mysql && useradd -r -g mysql mysql \

# Install Percona Mysql
&& yum install -y http://www.percona.com/downloads/percona-release/redhat/0.1-3/percona-release-0.1-3.noarch.rpm \
&& yum install -y Percona-Server-{client,devel,server,shared,test,tokudb}-56 \

# Clean up YUM when done.
&& yum clean all && rm -rf /var/lib/mysql && mkdir /var/lib/mysql \
&& chown -R mysql:mysql /var/lib/mysql && chmod -R 755 /var/lib/mysql

#COPY ./my.cnf /etc/my.cnf
COPY ./docker-entrypoint.sh /docker-entrypoint.sh

RUN chmod 775 /docker-entrypoint.sh

VOLUME ["/var/lib/mysql","/var/run/mysqld/"]

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 3306


CMD ["mysqld"]
