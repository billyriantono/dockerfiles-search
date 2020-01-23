FROM sysreport/basebox
MAINTAINER Thoralf Liersch <thoralf.liersch@sysreport.de>

COPY script/startup.sh /startup.sh

RUN set -x \
    && apk add --no-cache \
        mysql \
    && mkdir -p /var/lib/mysql \
    && { \
        echo '[mysqld]'; \
        echo 'user = root'; \
        echo 'datadir = /var/lib/mysql'; \
        echo 'port = 3306'; \
        echo 'log-bin = /var/lib/mysql/mysql-bin'; \
        echo 'binlog_format = ROW'; \
        echo 'skip_name_resolve = 1'; \
        echo 'collation_server = utf8_bin'; \
        echo 'socket = /var/lib/mysql/mysql.sock'; \
    } > /etc/mysql/my.cnf
CMD ["/startup.sh"]
