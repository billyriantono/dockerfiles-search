FROM nvidia/cuda:8.0-runtime-ubuntu16.04

MAINTAINER Kristoph Junge <kristoph.junge@gmail.com>

RUN apt-get update && \
    apt-get -y install ca-certificates curl --no-install-recommends && \
    rm -r /var/lib/apt/lists/*

RUN mkdir -p /opt/gominer

RUN curl -s -L -o /tmp/gominer.tar.gz https://github.com/decred/decred-binaries/releases/download/v1.0.0/gominer-linux-amd64-cuda-v1.0.0.tar.gz && \
    tar -xzf /tmp/gominer.tar.gz -C /opt/gominer && \
    mv /opt/gominer/gominer-linux-amd64-cuda*/* /opt/gominer/ && \
    rm -rf /opt/gominer/gominer-linux-amd64-cuda*

WORKDIR /opt/gominer

COPY docker-entrypoint.sh /docker-entrypoint.sh

CMD ["/docker-entrypoint.sh"]
