FROM mysql:5.7

ENV MYSQL_DATABASE=${MYSQL_DATABASE} \
    MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}

ADD wordpress_schema.sql /docker-entrypoint-initdb.d
#COPY sql_setter.sh /

#CMD ["/bin/bash", "/sql_setter.sh"]
EXPOSE 3306

