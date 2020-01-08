FROM alpine:latest

RUN apk add --no-cache postgresql-client
RUN touch ~/.pgpass \
    && chmod 600 ~/.pgpass

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
