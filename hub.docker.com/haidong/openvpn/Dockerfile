FROM ubuntu:16.10
MAINTAINER haidong <383623085@qq.com>

ARG OPENVPN_VERSION=2.1.9-Ubuntu16.amd_64

WORKDIR /tmp

RUN apt-get update && apt-get install -y curl iptables net-tools

RUN curl -O http://swupdate.openvpn.org/as/openvpn-as-${OPENVPN_VERSION}.deb \   
    && dpkg -i openvpn-as-${OPENVPN_VERSION}.deb \
    && echo "openvpn:Password01" | chpasswd

WORKDIR /root

EXPOSE 443/tcp 1194/udp 943/tcp

CMD ["/usr/local/openvpn_as/scripts/openvpnas","-n"]