FROM mysql
COPY . /docker-entrypoint-initdb.d
COPY pwd_setting.cnf /etc/mysql/conf.d/

ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_PASSWORD=example
ENV MYSQL_USER=narf
ENV MYSQL_DATABASE=dbname
