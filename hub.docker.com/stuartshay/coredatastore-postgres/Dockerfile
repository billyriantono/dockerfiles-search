FROM postgres:9.6

RUN apt-get update && apt-get install -y \
    postgresql-9.6-pgtap \
    postgresql-contrib-9.6  \
    postgresql-9.6-postgis-2.3-scripts \
    postgis \
&& rm -rf /var/lib/apt/lists/*

RUN mkdir -p /scripts 
RUN mkdir -p /tests
COPY scripts  /scripts
COPY tests  /tests
RUN chmod +x /scripts/PGPlaceholder.sh && mkdir -p /data
RUN chmod +x /tests/run-tests.sh 

COPY data  /data
COPY docker-entrypoint-initdb.d /docker-entrypoint-initdb.d

RUN echo "host all  all    0.0.0.0/0  md5" >> /var/lib/postgresql/data/pg_hba.conf && \
    echo "listen_addresses='*'" >> /var/lib/postgresql/data/postgresql.conf && \
    echo "shared_preload_libraries = 'pg_stat_statements'" >> /var/lib/postgresql/data/postgresql.conf && \
    echo "track_activity_query_size = 2048" >> /var/lib/postgresql/data/postgresql.conf && \
    echo "pg_stat_statements.track = all" >> /var/lib/postgresql/data/postgresql.conf 

