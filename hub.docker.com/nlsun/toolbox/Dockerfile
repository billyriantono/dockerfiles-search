FROM ubuntu:16.04

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        curl \
        dnsutils \
        hping3 \
        httpie \
        iperf \
        iproute2 \
        iptables \
        iputils-ping \
        ipvsadm \
        jq \
        net-tools \
        netcat \
        nmap \
        python3 \
        tcpdump \
        traceroute \
        tshark \
        wget \
        && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT []
CMD []
