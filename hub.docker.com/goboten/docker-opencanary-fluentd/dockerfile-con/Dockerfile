FROM debian:stable-slim

RUN apt-get update && \
    apt-get install -y curl dnsutils tcpdump && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
