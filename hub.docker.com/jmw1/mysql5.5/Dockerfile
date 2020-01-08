# Ubuntu 13.04 from Saltstack
# MySQL-5.5 Version 1

FROM stackbrew/ubuntu:13.10
RUN dpkg-divert --local --rename --add /sbin/initctl

RUN echo "deb http://archive.ubuntu.com/ubuntu saucy main universe" > /etc/apt/sources.list; apt-get update; echo "export HOME=/root\nalias l='ls -CF --color=auto --group-directories-first'\nalias la='ls -A --color=auto --group-directories-first'\nalias ll='ls -la --color=auto --group-directories-first'\nalias renv='. ~/.bashrc'\nalias vrc='vi ~/.bashrc'\nalias hst='perl ~/hst.pl $@'"


#RUN apt-get update  -  Would Cause Different Versions To Be Installed On Every Run
#RUN apt-get upgrade -y

RUN apt-get install -y mysql-client mysql-server

RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf

ADD http://localhost:8000/MySQLStart.sh /opt/MySQLStart.sh
ADD http://localhost:8000/hst.pl /root/

RUN chmod +x /opt/MySQLStart.sh;
EXPOSE 3306

CMD ["/bin/bash", "/opt/MySQLStart.sh"]
-----------------------------------


MySQLStart.sh File
-----------------------------------
#/bin/bash

if [ ! -f /var/lib/mysql/ibdata1 ]; then
    mysql_install_db

    /usr/bin/mysqld_safe &
    sleep 10s

    echo "GRANT ALL ON *.* TO admin@'%' IDENTIFIED BY 'changeme' WITH GRANT OPTION; FLUSH PRIVILEGES" | mysql

    killall mysqld
    sleep 10s
fi
/usr/bin/mysqld_safe
-----------------------------------

hst.pl File
-----------------------------------
#!/usr/bin/perl
use strict;
use warnings;

my $i = 1;
my $regex = '';
print "@ARGV\n";
print grep { /@ARGV/ } `cat ~/.bash_history`;
-----------------------------------

run-server.sh 
-----------------------------------
#!/bin/sh

docker run -d -p 3306:3306 -v /opt/mysqlData:/var/lib/mysql jmw1/mysql5.5:13.10
-----------------------------------

run-client.sh
-----------------------------------
#!/bin/sh

TAG="mysql"

CONTAINER_ID=$(docker ps | grep $TAG | awk '{print $1}')

IP=$(docker inspect $CONTAINER_ID | python -c 'import json,sys;obj=json.load(sys.stdin);print obj[0]["NetworkSettings"]["IPAddress"]')

mysql -u admin -p -h $IP
-----------------------------------
