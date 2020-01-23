FROM alpine

RUN apk --no-cache --update add dnsmasq

COPY config/dnsmasq.conf /etc/dnsmasq.conf

EXPOSE 53 53/udp

ENTRYPOINT ["dnsmasq", "-k", "-q", "--log-facility=-", "-d"]