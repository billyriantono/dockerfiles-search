FROM ubuntu:18.04

RUN apt-get update && apt install --no-install-recommends -y \
	libreswan netcat kmod && apt-get clean  && rm -rf /var/lib/apt/lists/* 

COPY entrypoint.sh entrypoint.sh
RUN chmod a+x entrypoint.sh

COPY sysctl.conf /etc/sysctl.conf

# Create required folders
RUN mkdir -p /var/run/pluto /etc/ipsec.d

RUN ipsec initnss

# ipsec - L2TP tunnel based VPN
EXPOSE 50/udp
EXPOSE 51/udp
EXPOSE 500/udp
EXPOSE 4500/udp

# ipsec - PPTP tunnel based VPN
EXPOSE 1723/tcp

VOLUME [ "/etc/ipsec.d"]
ENTRYPOINT [ "./entrypoint.sh" ]
