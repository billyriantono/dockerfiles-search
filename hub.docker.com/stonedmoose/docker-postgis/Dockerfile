# vim:set ft=dockerfile:
FROM mdillon/postgis:9.5

COPY docker-entrypoint.sh /usr/local/bin/
COPY ./initdb-postgis.sh /docker-entrypoint-initdb.d/postgis.sh
COPY ./update-postgis.sh /usr/local/bin

RUN chmod +x /usr/local/bin/docker-entrypoint.sh \
	     /docker-entrypoint-initdb.d/postgis.sh \
             /usr/local/bin/update-postgis.sh

CMD ["postgres"]
