FROM miko2u/centos6
MAINTAINER miko@cafelounge.net

# packages
RUN cd /tmp \
 && curl -OL http://repo.mysql.com/mysql-community-release-el6.rpm \
 && curl -OL http://packages.groonga.org/centos/groonga-release-1.1.0-1.noarch.rpm \
 && yum -y localinstall mysql-community-release-el6.rpm groonga-release-1.1.0-1.noarch.rpm \
 && yum -y install \
    mecab mecab-ipadic groonga groonga-tokenizer-mecab which logrotate \
    mysql-community-server mysql-community-client \
 && yum -y install mysql-community-mroonga \
 && yum -y update \
 && yum -y clean all \
 && rm -rf /tmp/*.rpm \
 && cp -pr /etc/my.cnf /etc/my.cnf.dist \
 && mkdir -p /var/log/mysql \
 && chown mysql:mysql /var/log/mysql \
 && chmod 750 /var/log/mysql \
 && chkconfig mysqld on

# configure
ADD my.cnf /etc/my.cnf
ADD mysqlbackup.cron /etc/cron.daily/
ADD mysql.logrotate /etc/logrotate.d/mysql
ADD boot/* /boot/
RUN chmod 700 /boot/prepare /boot/post \
 && chmod 755 /etc/cron.daily/mysqlbackup.cron

# expose
EXPOSE 3306
