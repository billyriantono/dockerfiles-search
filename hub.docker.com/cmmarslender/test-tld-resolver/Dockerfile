FROM alpine:edge
RUN apk --no-cache add dnsmasq
EXPOSE 53 53/udp

ENV DNS_FORWARD 8.8.8.8

CMD [ "sh", "-c", "dnsmasq -k -A /test/127.0.0.1 -S $DNS_FORWARD --log-facility=- --log-queries" ]
