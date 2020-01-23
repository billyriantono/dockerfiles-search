FROM debian:jessie

# Credits to jacksoncage/salt
MAINTAINER Hassan El Karhani <hkarhani@gmail.com>

# Update System
RUN DEBIAN_FRONTEND=noninteractive apt-get update -qq && \
    DEBIAN_FRONTEND=noninteractive apt-get install -yqq \
    wget git curl vim dnsutils python-pip \
    python-dev python-apt \
    software-properties-common dmidecode

# Install salt minion
RUN echo "deb http://repo.saltstack.com/apt/debian/8/amd64/latest jessie main" | tee /etc/apt/sources.list.d/saltstack.list && \
    wget -q -O- "https://repo.saltstack.com/apt/debian/8/amd64/latest/SALTSTACK-GPG-KEY.pub" | apt-key add - && \
    DEBIAN_FRONTEND=noninteractive apt-get update -qq && \
    DEBIAN_FRONTEND=noninteractive apt-get install -yqq salt-minion && \
    pip install docker-py

# Clean Image
RUN apt-get -yqq clean && \
    apt-get -yqq purge && \
    rm -rf /tmp/* /var/tmp/* && \
    rm -rf /var/lib/apt/lists/*
