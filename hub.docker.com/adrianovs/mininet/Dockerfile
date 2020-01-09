FROM ubuntu:latest
MAINTAINER Grupo6VR <adrianoseie@gmail.com>

COPY ENTRYPOINT.sh /

USER root
WORKDIR /root

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    iproute2 \
    iputils-ping \
    mininet \
    net-tools \
    tcpdump \
    wireshark \
    vim \
    x11-xserver-utils \
    xterm \
 && rm -rf /var/lib/apt/lists/* \
 && chmod +x /ENTRYPOINT.sh

EXPOSE 6633 6653

ENTRYPOINT ["/ENTRYPOINT.sh"]
