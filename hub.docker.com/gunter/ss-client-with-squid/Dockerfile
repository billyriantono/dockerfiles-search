FROM ubuntu:19.10

RUN apt-get update && apt-get upgrade -y && apt-get install iptables ipset curl squid shadowsocks-libev dnsutils iputils-ping iproute2 -y

ADD run.sh /root/
ADD set-iptables.sh /root/
ADD squid.conf /root/

RUN chmod +x /root/run.sh
RUN chmod +x /root/set-iptables.sh

ENV LOCAL_PORT 55555
EXPOSE 3128

ENTRYPOINT ["/root/run.sh"]