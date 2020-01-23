FROM avatao/ubuntu:14.04

# Install common packages
RUN apt-get -qy update \
    && apt-get -qy install \
        iproute2 \
        net-tools \
        nmap \
        tcpdump \
        tcpreplay \
        traceroute \
    && rm -rf /var/lib/apt/lists/*
