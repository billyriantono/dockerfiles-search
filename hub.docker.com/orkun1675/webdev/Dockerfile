# Simple Ubuntu with Networking tools installed.
# Useful for kubernetes debugging.
# Author: orkun1675

FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
  vim \
  rsyslog \
  nmap \
  iputils-ping \
  traceroute \
  iproute2 \
  net-tools \
  curl \
  tcpdump \
  iptables \
  kmod \
  tmux \
  screen \
  netcat \
  dnsutils \
  && rm -rf /var/lib/apt/lists/* \
  && sed -e '/$KLogPermitNonKernelFacility/ s/^#*/# /' -i /etc/rsyslog.conf \
  && service rsyslog restart

CMD ["/bin/bash"]

LABEL version="1.0"
