
## This Dockerfile creates a Debian container with tools for network checking.
##
## Details available at https://bitbucket.org/arbiza/net-check-tools
## -----------------------------------------------------------------------------

## Use Debian image
FROM debian:jessie

LABEL mantainer="Lucas Arbiza" description="Network Verification tools"

## Update the system and install packages
RUN apt-get update && apt-get install -y \
    dnsutils \
    hping3 \
    mtr \
    sipcalc \
    tcpdump \
    traceroute \
    whois
