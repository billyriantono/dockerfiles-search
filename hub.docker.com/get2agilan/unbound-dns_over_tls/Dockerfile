FROM alpine:latest

RUN apk --no-cache add unbound ca-certificates

COPY unbound.conf /etc/unbound/unbound.conf

RUN ln -sf /dev/stdout /var/log/unbound.log

EXPOSE 53/udp 53/tcp

ENTRYPOINT ["unbound", "-d"]