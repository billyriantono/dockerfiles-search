FROM balenalib/armv7hf-debian:stretch

RUN [ "cross-build-start" ]


RUN apt-get update && apt-get install openssl unbound wget ldnsutils

RUN wget -O /var/lib/unbound/root.hints https://www.internic.net/domain/named.root

COPY unbound.conf /etc/unbound/unbound.conf

HEALTHCHECK --interval=60s --timeout=10s --start-period=5s CMD drill @127.0.0.1 -p 5353 cloudflare.com || exit 1

EXPOSE 5353/udp

ENTRYPOINT ["/usr/sbin/unbound"]

CMD ["-c", "/etc/unbound/unbound.conf", "-d"]

RUN [ "cross-build-end" ]  
