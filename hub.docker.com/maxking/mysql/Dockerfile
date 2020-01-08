FROM mysql:latest

RUN { \
      echo '[mysqld]'; \
      echo 'character-set-server=utf8'; \
      echo 'collation-server=utf8_general_ci'; \
      echo '[client]'; \
      echo 'default-character-set=utf8'; \
    } > /etc/mysql/conf.d/charset.cnf

ENV MYSQL_ROOT_PASSWORD runner
ENV MYSQL_USER runner
ENV MYSQL_USER_PASSWORD runner
ENV MYSQL_DATABASE test_mailman

EXPOSE 3306
CMD ["mysqld"]
