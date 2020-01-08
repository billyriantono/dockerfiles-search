FROM ubuntu:15.10
MAINTAINER Georg Kunz, CloudGear <contact@cloudgear.net>

RUN apt-get update -q && apt-get install -yq --no-install-recommends \
        ca-certificates \
        curl \
        wget \
        dnsutils \
        iputils-ping \
        telnet \
        net-tools \
        netcat \
        tcpdump \
        git && \

    # clean up
    rm -rf /var/lib/apt/lists/* && \
    truncate -s 0 /var/log/*log

ENTRYPOINT ["/bin/bash"]
