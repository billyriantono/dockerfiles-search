FROM alpine

RUN apk add --no-cache dnsmasq

EXPOSE 53 53/udp
ENTRYPOINT ["dnsmasq", "--keep-in-foreground", "--log-queries", "--log-facility=-"]
