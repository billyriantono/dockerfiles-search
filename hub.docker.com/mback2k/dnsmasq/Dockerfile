FROM mback2k/debian:stretch

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        dnsmasq && \
    apt-get clean

VOLUME /etc/dnsmasq

CMD ["/usr/sbin/dnsmasq", "-d", "-u", "dnsmasq"]
