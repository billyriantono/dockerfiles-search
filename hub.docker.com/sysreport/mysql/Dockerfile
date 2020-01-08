FROM sysreport/devbox:latest
MAINTAINER Thoralf Liersch <thoralf.liersch@sysreport.de>

WORKDIR /var/lib/mysql
COPY startup.sh /startup.sh

RUN set -x \
    && apk add --no-cache \
        mysql \
    && mkdir -p /var/lib/mysql \
    && mkdir -p /etc/mysql/conf.d \
    && { \
        echo '[mysqld]'; \
        echo 'user = root'; \
        echo 'datadir = /var/lib/mysql'; \
        echo 'port = 3306'; \
        echo 'log-bin = /var/lib/mysql/mysql-bin'; \
        echo 'binlog_format = ROW'; \
        echo 'socket = /var/lib/mysql/mysql.sock'; \
        echo '!includedir /etc/mysql/conf.d/'; \
    } > /etc/mysql/my.cnf
CMD ["/startup.sh"]
