FROM alpine:3.8

ARG MARIADB_VERSION=10.2.15
ENV MYSQL_HOST=mysql

COPY src /
RUN mariadb-client-setup
ENTRYPOINT ["mariadb-client-entrypoint"]
CMD ["mysql"]
