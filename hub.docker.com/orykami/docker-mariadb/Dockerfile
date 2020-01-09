# MariaDB Dockerfile
# https://github.com/orykami/docker-mariadb
FROM mariadb:latest
# Copying default MariaDB configuration file into container
COPY config/mariadb.cnf /etc/mysql/mariadb.cnf
COPY config/my.cnf /etc/mysql/my.cnf
# Running mariadb-server with our custom configuration file
CMD ["mysqld"]