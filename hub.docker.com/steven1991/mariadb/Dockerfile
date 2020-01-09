FROM webhippie/mariadb:latest
Maintainer Steven Schramm <steven.schramm91@googlemail.com>
COPY my.cnf /etc/mysql/my.cnf
COPY source_secrets.sh /etc/entrypoint.d/source_secrets.sh
COPY healthcheck /usr/bin/healthcheck
COPY mysqldump.sh /tmp/mysqldump.sh
