FROM alpine:3.7

RUN apk update
RUN apk add dnsmasq

COPY dnsmasq.conf /etc/
COPY resolv.dnsmasq.conf /etc/

VOLUME /dnsmasq.hosts

EXPOSE 5353

ENTRYPOINT ["/usr/sbin/dnsmasq", "-d"]

