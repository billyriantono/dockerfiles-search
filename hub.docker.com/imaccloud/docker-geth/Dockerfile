FROM ubuntu:wily

# Based on https://github.com/vallard/ethereum-infrastructure/tree/master/Docker
MAINTAINER Kyle Bai (kyle.b@inwinstack.com)

# Install ethereum and dependency packages
RUN apt-get update && \
    apt-get install -q -y git curl software-properties-common vim && \
    add-apt-repository ppa:ethereum/ethereum && \
    add-apt-repository ppa:ethereum/ethereum-dev && \
    apt-get update && apt-get install -q -y geth

# Copy ethereum data to container
COPY ethereum /opt/ethereum
COPY boot_run.sh /etc/boot_run.sh
RUN chown root.root /etc/boot_run.sh && chmod 700 /etc/boot_run.sh

VOLUME ["/opt/ethereum/ethdata"]
WORKDIR /opt/ethereum
EXPOSE 8545 30303

ENTRYPOINT ["/etc/boot_run.sh"]
