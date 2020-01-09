FROM debian:9.7
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive \
    && apt-get install --no-install-recommends -y apt-mirror \
    && mkdir -p /Data \
    && rm -rf /var/lib/apt/lists/*

VOLUME /Data
WORKDIR /Data

CMD ["/usr/sbin/apt-mirror","mirror.list"]
