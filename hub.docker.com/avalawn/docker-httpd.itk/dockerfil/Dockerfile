FROM debian:wheezy

ENV DNSMASQ_OPTS -8-
ENV DNSMASQ_USER root

RUN apt-get update \
 && echo 'exit 101' | install -m 755 /dev/stdin /usr/sbin/policy-rc.d \
 && DEBIAN_FRONTEND=noninteractive apt-get -y install dnsmasq \
 && update-rc.d -f dnsmasq remove \
 && rm -f /usr/sbin/policy-rc.d \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 53/udp
CMD ["/etc/init.d/dnsmasq", "systemd-exec"]
