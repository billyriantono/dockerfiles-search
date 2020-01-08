FROM debian:stretch-slim

ENV DEBIAN_FRONTEND=noninteractive

# update
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils systemd

# generic tools
RUN apt-get install -y vim wget net-tools git unzip curl iputils-ping telnet dnsutils nmap \
    software-properties-common apt-transport-https lsb-release ca-certificates gnupg2