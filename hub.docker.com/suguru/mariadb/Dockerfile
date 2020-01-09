FROM alpine

RUN apk --update --no-cache add mysql

COPY ./my.cnf /etc/mysql/my.cnf
RUN mysql_install_db --user=mysql

COPY ./init.sql /init.sql
RUN mysqld --user=mysql --bootstrap < /init.sql

EXPOSE 3306
VOLUME ["/var/lib/mysql"]
ENTRYPOINT ["/usr/bin/mysqld", "--user=mysql", "--console"]
