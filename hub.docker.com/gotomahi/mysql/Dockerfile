FROM mysql:8 as builder
RUN ["sed", "-i", "s/exec \"$@\"/echo \"not running $@\"/", "/usr/local/bin/docker-entrypoint.sh"]
ENV MYSQL_ROOT_PASSWORD=p@ssw0rd
COPY src/scripts/**/*.sql /docker-entrypoint-initdb.d/
RUN ["/usr/local/bin/docker-entrypoint.sh", "mysqld", "--datadir", "/initialized-db"]
FROM mysql:8

COPY --from=builder /initialized-db /var/lib/mysql
EXPOSE 0.0.0.0:3306:3306