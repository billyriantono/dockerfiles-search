FROM alpine:edge

RUN apk --no-cache --progress add pgbouncer

COPY pgbouncer.ini /etc/pgbouncer/pgbouncer.ini
COPY entrypoint.sh /

EXPOSE 6432

ENTRYPOINT ["/entrypoint.sh"]
CMD ["-u", "pgbouncer", "/etc/pgbouncer/pgbouncer.ini"]
