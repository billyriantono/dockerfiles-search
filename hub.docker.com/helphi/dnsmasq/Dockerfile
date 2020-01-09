FROM alpine:3.10.0

RUN apk --no-cache add dnsmasq=2.80-r3

VOLUME /etc/dnsmasq.d

EXPOSE 53 53/udp 67/udp 68/udp

CMD ["dnsmasq", "-k"]