FROM alpine:3.9

# add Tini (a simple init; ensures that zombie processes are reaped properly)
RUN apk --update add --no-cache tini
ENTRYPOINT ["/sbin/tini", "--"]

RUN apk add --no-cache mongodb-tools

COPY backup.sh /backup.sh
COPY entrypoint.sh /entrypoint.sh

VOLUME /backups

CMD ["/entrypoint.sh"]
