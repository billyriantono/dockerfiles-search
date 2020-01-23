FROM alpine

RUN ["apk", "update"]
RUN ["apk", "upgrade", "--available"]

RUN ["apk", "add", \
      "iptables", \
      "tcpdump"]

RUN echo 'ipv6' >> /etc/modules
RUN echo 'net.ipv6.conf.all.disable_ipv6 = 1' >> /etc/sysctl.d/01-disable-ipv6.conf

ADD enable_nat.sh /enable_nat.sh
CMD ["/bin/sh", "/enable_nat.sh"]
