FROM postgres:11.5-alpine

# 1 - Add replication from all sources
COPY ./docker-entrypoint-initdb.d/01-add_replication_for_all_sources.sh /docker-entrypoint-initdb.d/
