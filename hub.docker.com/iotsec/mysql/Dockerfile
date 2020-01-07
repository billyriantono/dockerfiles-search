#FROM lsioarmhf/mariadb
FROM linuxserver/mariadb:arm32v7-latest

HEALTHCHECK --interval=1m30s CMD mysql -u $MYSQL_USER --password=$MYSQL_USER_PASSWORD iotsec -e  'SELECT * FROM user;'

COPY iotsec.sql /docker-entrypoint-initdb.d/iotsec.sql
COPY 50-init-iotsec /etc/cont-init.d/50-init-iotsec
