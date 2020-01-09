FROM ubuntu:xenial

MAINTAINER ungleich Team "docker@ungleich.ch"

RUN apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install \
	                  --no-install-recommends -y \
                      -o Dpkg::Options::="--force-confdef" \
                      -o Dpkg::Options::="--force-confold" \
                        git \
                        openssl \
                        ca-certificates \
                        openssh-client \
                        curl \
                        dnsutils \
                        iputils-ping \
                        iproute \
                        tftp \
                        tshark \
                        man \
                        nmap \
                        dsniff \
                        socat \
                        netcat \
                        zsh \
                        dhcping \
                        udhcpc \
                        dhcpdump \
                        dhcpcd5 \
                        python3 \
                        vim \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*
