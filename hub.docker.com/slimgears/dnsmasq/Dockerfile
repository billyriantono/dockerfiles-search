FROM alpine:edge
RUN apk --no-cache add dnsmasq
EXPOSE 53 53/udp 67/udp 68/udp 69/udp
ENTRYPOINT ["dnsmasq", "-k", "--log-facility=-"]
