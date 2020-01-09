FROM alpine:3.10

RUN adduser -DHs /bin/false opendkim &&\
    mkdir -p /run/opendkim &&\
    chown opendkim:opendkim /run/opendkim

RUN apk add --no-cache opendkim ca-certificates

EXPOSE 8891

CMD ["/usr/sbin/opendkim", "-fx", "/etc/opendkim/opendkim.conf"]
