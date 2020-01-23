FROM ubuntu:latest
RUN apt-get update && apt-get install -y dnsmasq
#ADD dnsmasq.conf /etc/dnsmasq.conf
EXPOSE 53/udp
ENTRYPOINT ["/usr/sbin/dnsmasq", "--no-daemon"]
