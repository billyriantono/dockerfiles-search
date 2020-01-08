FROM percona:psmdb-4.0.10

ENV MONGO_INITDB_DATABASE foobar

# 1 - Add foobar database with some data from MorngoDB
COPY ./data /data
COPY ./docker-entrypoint-initdb.d/01-add_foobar_data.sh /docker-entrypoint-initdb.d/
