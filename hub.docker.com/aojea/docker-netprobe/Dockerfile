FROM alpine:3.6
MAINTAINER A.Ojea <antonio.ojea.garcia@gmail.com>

RUN apk update && \
    apk add bash curl scapy \
    tcpdump iperf nmap && \
    rm -rf /var/cache/apk/*
