FROM azmo/base:debian-slim
LABEL maintainer "Gordon Schulz <gordon.schulz@gmail.com>"

RUN apt-get update && apt-get -y --no-install-recommends install openvpn \
        iptables iputils-ping iputils-tracepath traceroute grep \
        iproute2 curl ca-certificates ufw procps ipcalc && apt-get clean && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD rootfs /
VOLUME /etc/openvpn/config
