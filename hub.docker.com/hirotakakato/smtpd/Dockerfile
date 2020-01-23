FROM alpine:latest

RUN set -eux; \
    apk add --no-cache ca-certificates opensmtpd; \
    echo -e 'listen on 0.0.0.0\naccept from any for any relay' > /etc/smtpd/smtpd.conf; \
    install -m 711 -d /var/spool/smtpd

VOLUME ["/var/spool/smtpd"]

CMD ["smtpd", "-d"]

EXPOSE 25
