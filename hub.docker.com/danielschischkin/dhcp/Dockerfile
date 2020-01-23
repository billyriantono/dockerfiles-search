FROM alpine:latest

EXPOSE 67

COPY files/dhcpd.conf /etc/dhcp/dhcpd.conf

RUN mkdir -p /var/lib/dhcp && \
    touch /var/lib/dhcp/dhcpd.leases

RUN apk update && apk add dhcp

ENTRYPOINT [ "dhcpd", "-4", "-d" ]