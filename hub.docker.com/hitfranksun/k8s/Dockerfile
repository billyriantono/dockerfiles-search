FROM ubuntu:16.04

LABEL maintainer Franksun

RUN apt-get update || true && \
    apt-get install -y \
    curl wget \
    pkg-config && \
    rm -rf /var/lib/dpkg/info/* /var/lib/apt/lists/*

RUN wget -c https://github.com/heketi/heketi/releases/download/v9.0.0/heketi-client-v9.0.0.linux.amd64.tar.gz

CMD ["/bin/bash"]
