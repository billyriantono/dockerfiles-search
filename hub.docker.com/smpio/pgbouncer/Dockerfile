FROM alpine

RUN apk add --no-cache pgbouncer su-exec

ENTRYPOINT ["su-exec", "pgbouncer", "pgbouncer"]
