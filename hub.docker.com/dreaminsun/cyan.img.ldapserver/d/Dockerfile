FROM debian:9-slim

RUN DEBIAN_FRONTEND=noninteractive && \
    apt-get update -q && \
    apt-get upgrade -y && \
    apt-get install -y wget && \
    apt-get clean -y && \
    rm -rf /var/lib/apt

RUN wget -q -O /tini https://github.com/krallin/tini/releases/download/v0.18.0/tini-amd64 && \
    chmod +x /tini

ENTRYPOINT ["/tini", "--"]