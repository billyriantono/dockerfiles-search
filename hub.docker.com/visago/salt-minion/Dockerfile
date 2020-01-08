FROM ubuntu:18.04
RUN apt-get update && \
    apt-get install -y \
        jq \
        wget \
        mtr \
        fping \
        nmap \
        curl \
        git \
        cmake \
        unzip \
        iproute2 \
        apt-transport-https \
        ca-certificates \
        software-properties-common \
        gnupg \
        libffi-dev \
        libssl-dev \
        python-pip \
        python-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN curl -L https://bootstrap.saltstack.com -o install_salt.sh && sh install_salt.sh -P
CMD ["/usr/bin/salt-minion", "-l", "info"]
