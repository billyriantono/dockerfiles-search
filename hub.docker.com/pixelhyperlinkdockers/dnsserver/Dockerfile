# PixelHyperlink DNS Server Docker
#
# VERSION               1.0.0

FROM pixelhyperlinkdockers/ubuntu:v1.8.0
MAINTAINER Abhishek Salian <abhi@pixelhyperlink.com>

LABEL Description="This image contains base ubuntu os with bind service."
LABEL Vendor="PixelHyperlink"
LABEL Version="1.0.0"
LABEL com.pixelhyperlink.docker.phpserver.version="1.0.0"
LABEL vendor="PixelHyperlink"
LABEL com.pixelhyperlink.docker.dnsserver.release-date="2017-07-24"
LABEL com.pixelhyperlink.docker.dnsserver.version.is-production="true"

# Expose apache.
EXPOSE 53 10000

# Install bind
RUN apt-get update && \
	apt-get install -y bind9 \
	bind9utils \
	bind9-doc

RUN mkdir /etc/bind/zones

COPY ./bind9 /etc/default/bind9

COPY ./named.conf.options /etc/bind/named.conf.options

COPY ./named.conf.local /etc/bind/named.conf.local

COPY ./pixelhyperlink_zones.conf /etc/bind/pixelhyperlink_zones.conf

COPY ./pixelhyperlink.lan.conf /etc/bind/zones/pixelhyperlink.lan.conf

# Copy server dns start up scripts
COPY ./dns_entrypoint.sh /opt/dns_entrypoint.sh

# Run dns startup scripts
RUN chmod 755 /opt/dns_entrypoint.sh

ENTRYPOINT ["/opt/dns_entrypoint.sh"]
