FROM ubuntu:bionic

MAINTAINER 33b5e5 <33b5e5@users.noreply.github.com>

RUN apt-get update \
  && apt-get install -y curl dnsutils htop iproute2 iputils-ping \
    netcat-openbsd net-tools nmap tcpdump telnet traceroute wget whois \
  && rm -rf /var/lib/apt/lists/*

COPY Dockerfile /Dockerfile

LABEL org.label-schema.docker.dockerfile="/Dockerfile" \
  org.label-schema.vcs-type="Git" \
  org.label-schema.vcs-url="https://github.com/33b5e5/ubuntu-network-utils"
