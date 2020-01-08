FROM mysql:5.6
ENV MYSQL_ROOT_PASSWORD changeme
ENV MYSQL_DATABASE nobotgames

COPY ./dump.sql /docker-entrypoint-initdb.d/
