FROM alpine:3.8

RUN apk add --no-cache postgresql
ADD loop.sh /

ENV POSTGRES_USER=postgres
ENV POSTGRES_DATABASE=postgres
ENV POSTGRES_PORT=5432
ENV INTERVAL=3600

ENTRYPOINT ["/loop.sh"]


