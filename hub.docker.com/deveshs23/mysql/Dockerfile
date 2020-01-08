FROM mysql/mysql-server:5.7
COPY my.cnf /etc/my.cnf
COPY root-config.sql /docker-entrypoint-initdb.d/root-config.sql
ENV MYSQL_ROOT_HOST '%' 
ENV MYSQL_ROOT_PASSWORD '123456'
ENV MYSQL_DATABASE inventorywms
