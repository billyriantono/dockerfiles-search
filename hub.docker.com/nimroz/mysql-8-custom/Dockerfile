# Derived from official mysql image (our base image)
FROM mysql:8.0

RUN sed -i '/^\[mysqld\]$/a\default-authentication-plugin=mysql_native_password' /etc/mysql/my.cnf
RUN sed -i '/^\[mysqld\]$/a\local-infile=1' /etc/mysql/my.cnf

CMD ["mysqld"]
