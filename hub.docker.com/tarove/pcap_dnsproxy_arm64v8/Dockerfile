FROM multiarch/debian-debootstrap:arm64-sid-slim as builder

RUN set -ex &&\
    apt-get update && \
    apt-get install -y git \
                       build-essential \
                       cmake \
                       libsodium-dev \
                       libpcap-dev \
                       libssl-dev \
                       libevent-dev \
                       flex \
                       bison

RUN cd /tmp && \
        git clone --depth=1 https://github.com/chengr28/Pcap_DNSProxy.git /tmp/Pcap_DNSProxy && \
        cd /tmp/Pcap_DNSProxy/Source/Auxiliary/Scripts && \
        sh CMake_Build.sh && \
        mv /tmp/Pcap_DNSProxy/Source/Release /pcap_dnsproxy && \
        chmod +x /pcap_dnsproxy/Pcap_DNSProxy


FROM multiarch/debian-debootstrap:arm64-sid-slim

WORKDIR /pcap_dnsproxy
ENV TZ 'Asia/Shanghai'

RUN set -ex &&\
    apt-get update && \
    apt-get install -y \
                       libsodium23 \
                       libevent-dev \
                       libpcap0.8 && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo $TZ > /etc/timezone
    
COPY --from=builder /pcap_dnsproxy /pcap_dnsproxy

WORKDIR /pcap_dnsproxy
ENTRYPOINT ["/pcap_dnsproxy/Pcap_DNSProxy", "--disable-daemon"]