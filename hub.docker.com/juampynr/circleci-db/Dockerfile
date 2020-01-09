FROM mariadb:10.4 as builder

RUN ["sed", "-i", "s/exec \"$@\"/echo \"not running $@\"/", "/usr/local/bin/docker-entrypoint.sh"]

ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=wikimedia_images

RUN apt-get update && \
  apt-get install --yes wget && \
  wget https://dumps.wikimedia.org/enwiki/latest/enwiki-latest-image.sql.gz && \
  gunzip enwiki-latest-image.sql.gz && \
  mv enwiki-latest-image.sql docker-entrypoint-initdb.d

RUN ["/usr/local/bin/docker-entrypoint.sh", "mysqld", "--datadir", "/initialized-db", "--aria-log-dir-path", "/initialized-db"]

FROM mariadb:10.4

COPY --from=builder /initialized-db /var/lib/mysql
