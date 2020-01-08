FROM mysql:8

RUN echo '[mysqld]' >> /etc/mysql/conf.d/mysql.cnf \
&&  echo 'default-authentication-plugin = mysql_native_password' >> /etc/mysql/conf.d/mysql.cnf \
&&  echo 'collation-server = utf8mb4_unicode_ci' >> /etc/mysql/conf.d/mysql.cnf \
&&  echo 'character-set-server = utf8mb4' >> /etc/mysql/conf.d/mysql.cnf