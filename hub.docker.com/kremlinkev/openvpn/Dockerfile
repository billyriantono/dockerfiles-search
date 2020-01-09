FROM ubuntu:latest

ARG DEBIAN_FRONTEND="noninteractive"

RUN apt-get update && \
    apt-get install -y openvpn \
                       ca-certificates \
                       curl \
                       iptables

RUN echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf
VOLUME /config
