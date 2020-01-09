FROM alpine:3.8
LABEL maintainer="futamint"

RUN apk add --no-cache \
        curl \
        unbound

RUN curl ftp://ftp.internic.net/domain/named.cache > /etc/unbound/root.hints

COPY unbound/ /etc/unbound/

CMD ["/usr/sbin/unbound", "-d", "-c", "/etc/unbound/unbound.conf"]

EXPOSE 53
