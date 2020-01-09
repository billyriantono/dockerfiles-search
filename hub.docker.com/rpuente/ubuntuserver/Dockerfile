FROM ubuntu:xenial

RUN apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y \
      arping \
      arp-scan \
      bind9-host \
      curl \
      dhcping \
      dnsutils \
      iptables \
      iputils-ping \
      mtr \
      net-tools \
      nmap \
      tcpdump \
      telnet \
      tftp-hpa \
      traceroute \
	  netcat \
	  vim \
      wget && \
    apt-get clean && \
    rm -rvf /var/lib/apt/lists/*

HEALTHCHECK CMD ["ls"]

COPY run.sh /opt
RUN chmod +x /opt/run.sh

CMD /opt/run.sh