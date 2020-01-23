FROM ubuntu
MAINTAINER Clark Laughlin clark@laughlins.org

RUN apt-get update
RUN apt-get install -y dnsmasq supervisor

RUN mkdir -p /srv/dnsmasq
RUN touch /srv/dnsmasq/resolv.conf

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD dnsmasq.conf /etc/dnsmasq.conf

VOLUME /srv/dnsmasq

# DNS: TCP/UDP port 53
EXPOSE 53

CMD ["/usr/bin/supervisord"]
