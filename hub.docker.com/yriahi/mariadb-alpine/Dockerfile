FROM alpine:latest
MAINTAINER Youssef Riahi <y.riahi@gmail.com>

ENV DB_DATA_PATH="/var/lib/mysql"

# Update & upgrade Alpine linux
RUN apk update && apk upgrade

# Install MariaDB
RUN apk add --no-cache mariadb mariadb-client
RUN mkdir -p /run/mysqld
RUN chown -R mysql:mysql /run/mysqld
RUN mysql_install_db --user=mysql --datadir=${DB_DATA_PATH}
COPY my.cnf /etc/mysql/my.cnf
RUN chown mysql:mysql /etc/mysql/my.cnf

# Listen on
EXPOSE 3306

# start mysqld server
ENTRYPOINT ["mysqld_safe", "--user=mysql"]
