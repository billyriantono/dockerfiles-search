FROM alpine:latest

RUN apk add --update bash gzip openssh-client rsync && \
    rm -rf /var/cache/apk/*

ENV BACKUP_TIME 0 3 * * *

COPY entrypoint.sh /scripts/entrypoint.sh
COPY backup.sh /scripts/backup.sh

ENTRYPOINT ["/scripts/entrypoint.sh"]

CMD ["/usr/sbin/crond", "-f", "-d", "0"]
