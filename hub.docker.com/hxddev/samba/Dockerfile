FROM alpine

RUN apk add samba

EXPOSE 139 445

VOLUME ["/etc/samba"]

COPY docker-entrypoint.sh /bin/
ENTRYPOINT ["docker-entrypoint.sh"]