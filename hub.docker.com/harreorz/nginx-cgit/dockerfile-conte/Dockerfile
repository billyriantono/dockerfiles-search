FROM ubuntu:bionic

ENV DEBIAN_FRONTEND=noninteractive

RUN rm /etc/dpkg/dpkg.cfg.d/excludes &&\
        apt-get update &&\
        apt-get -y --no-install-recommends install\
        vim less sudo curl wget man jq ca-certificates\
        net-tools iproute2 dnsutils netcat-openbsd strace gdb file &&\
        rm -r /var/lib/apt/lists/*

