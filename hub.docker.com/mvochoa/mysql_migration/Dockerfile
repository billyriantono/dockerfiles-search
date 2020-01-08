FROM mysql:5.6

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y gettext
COPY docker-entrypoint-migrate.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint-migrate.sh /entrypoint-migrate.sh

WORKDIR /docker-entrypoint-migrate.d
VOLUME /docker-entrypoint-migrate.d

CMD sh -c "docker-entrypoint-migrate.sh"