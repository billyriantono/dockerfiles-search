FROM ubuntu:bionic

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
      openssl \
    && apt-get clean

WORKDIR /certs

ENTRYPOINT ["/usr/bin/openssl"]