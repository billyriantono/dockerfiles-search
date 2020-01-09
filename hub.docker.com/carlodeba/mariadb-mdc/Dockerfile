FROM mariadb
COPY custom.cnf /etc/mysql/conf.d
COPY backup-mysql.sh /root
COPY startup.sh /
COPY backup-mysql-cron /root
RUN chmod 755 /root/backup-mysql.sh
RUN chmod 755 /startup.sh
RUN apt-get update
RUN apt-get install cron
ENV MYSQL_ROOT_PASSWORD tHeRo0TpWd
ENV MYSQL_DATABASE theDatabase
ENV MYSQL_USER theUser
ENV MYSQL_PASSWORD tH3p@sSwD
ENTRYPOINT ["/startup.sh"]
