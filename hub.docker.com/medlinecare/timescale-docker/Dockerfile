# Version 2.0

FROM timescale/timescaledb:1.5.1-pg11

RUN apk add --update tzdata

#Deben inicializarse/personalizarse en el docker-compose.yml
#ENV TZ Europe/Madrid
#ENV POSTGRES_INITDB_ARGS --locale=es_ES
#ENV POSTGRES_USER postgres
#ENV POSTGRES_PASSWORD
#ENV DB_NAME medlinecare
#ENV DB_USER medlinetec
#ENV DB_PASS
#ENV PGDATA /var/lib/postgresql/data

COPY setup_database.sh /docker-entrypoint-initdb.d/setup_database.sh
RUN chmod 755 /docker-entrypoint-initdb.d/setup_database.sh

  
