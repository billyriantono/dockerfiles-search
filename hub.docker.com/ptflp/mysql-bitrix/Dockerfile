FROM mariadb:10.3
COPY ./bx_mysql.cnf /etc/mysql/conf.d
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld"]