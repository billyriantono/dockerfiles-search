FROM mysql:5.7

ENV MYSQL_CONFDIR /etc/mysql/conf.d

RUN { \
    echo '[mysqld]'; \
    echo 'sql_mode=NO_ENGINE_SUBSTITUTION'; \
} | tee "${MYSQL_CONFDIR}/mtc-material.cnf"
