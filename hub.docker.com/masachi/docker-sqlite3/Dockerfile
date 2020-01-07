FROM alpine:3.4

RUN apk update \
    && apk add sqlite \
    && apk add socat

RUN mkdir -p /root/db

WORKDIR /root/db
ENTRYPOINT [ "sqlite3" ]
