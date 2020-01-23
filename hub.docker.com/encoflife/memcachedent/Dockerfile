FROM wrouesnel/postgres_exporter:v0.8.0

COPY queries.yaml /queries.yaml

ENV PG_EXPORTER_EXTEND_QUERY_PATH=/queries.yaml
