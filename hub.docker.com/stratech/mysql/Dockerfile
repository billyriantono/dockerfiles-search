#++++++++++++++++++++++++++++++++++++++
# stratech/mysql
#++++++++++++++++++++++++++++++++++++++
# Mysql Docker container   
#++++++++++++++++++++++++++++++++++++++

FROM stratech/ubuntu:14.04
MAINTAINER Stefano Mazzega <stefano.mazzega@gmail.com>

CMD ["/sbin/my_init"]

# Some Environment Variables
ENV    DEBIAN_FRONTEND noninteractive

RUN sed -i "s/^exit 101$/exit 0/" /usr/sbin/policy-rc.d

# Ensure UTF-8
ENV LANG       en_US.UTF-8
ENV LC_ALL     en_US.UTF-8

# MySQL ENV
ENV MYSQL_USER=mysql
ENV MYSQL_DATA_DIR=/var/lib/mysql
ENV MYSQL_RUN_DIR=/run/mysqld
ENV MYSQL_LOG_DIR=/var/log/mysql
ENV MYSQL_SCRIPT_DIR=/var/lib/mysql/setup
ENV DB_REMOTE_ROOT_NAME=root
ENV DB_REMOTE_ROOT_PASS=root
ENV MYSQL_CHARSET: 'utf8'
ENV MYSQL_COLLATION: 'utf8_general_ci'

# MySQL Installation
RUN apt-get update
RUN echo "mysql-server mysql-server/root_password password root" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password root" | debconf-set-selections
RUN apt-get update && apt-get install -y --force-yes mysql-server-5.6 pwgen curl

ADD etc/my_init.d/99_mysql_setup.sh /etc/my_init.d/99_mysql_setup.sh
RUN chmod +x /etc/my_init.d/99_mysql_setup.sh

ADD build/import_db.sh /sbin/import_db.sh
RUN chmod +x /sbin/import_db.sh

EXPOSE 3306
EXPOSE 22

RUN mkdir -p /etc/service/mysql
ADD build/start.sh /etc/service/mysql/run
RUN chmod +x /etc/service/mysql/run

# END MySQL Installation

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*