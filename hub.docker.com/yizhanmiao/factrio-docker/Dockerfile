FROM ubuntu:18.04

RUN apt update && apt install -y openssh-server openssh-client curl && \
    apt-get clean && apt-get autoremove

RUN curl -L https://www.factorio.com/get-download/0.16.51/headless/linux64 -o factorio.tar.xz&& \
    tar -xf factorio.tar.xz -C /opt && \
    rm factorio.tar.xz

ENV PATH="/opt/factorio/bin/x64:$PATH"

EXPOSE 22/udp
EXPOSE 27015/tcp
