FROM debian:latest
MAINTAINER Hǎiliàng Wáng <w@h12.me>

RUN apt-get update && apt-get install -y dnsmasq --no-install-recommends

ENTRYPOINT ["/usr/sbin/dnsmasq", "-k"]
