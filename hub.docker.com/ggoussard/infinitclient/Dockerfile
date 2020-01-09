FROM debian:jessie

RUN groupadd -r infinit && \
    useradd -r -g infinit infinit && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3D2C3B0B && \
    apt-get update && \
    apt-get install -y \
        software-properties-common \
        apt-transport-https && \
    add-apt-repository "deb https://debian.infinit.sh/ trusty main" && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
        fuse \
        infinit && \
    apt-get clean -y && \
    apt-get autoclean -y && \
    apt-get autoremove -y && \
    rm -rf /usr/share/locale/* \
           /var/cache/debconf/*-old \
           /var/lib/apt/lists/* \
           /usr/share/doc/*

USER infinit
VOLUME /mnt/shared
WORKDIR /opt/infinit
COPY entrypoint.sh entrypoint.sh

ENTRYPOINT ["sh", "entrypoint.sh"]
