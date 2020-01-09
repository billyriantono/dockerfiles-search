FROM ubuntu:18.04

LABEL maintainer="Di Mou <moudi717@live.com>" \
      image="moudixtc/shadowsocks:latest"

RUN apt-get update && \
    apt-get install -y curl git python3 python3-distutils && \
    curl -sSL https://bootstrap.pypa.io/get-pip.py | python3

RUN pip3 install git+https://github.com/shadowsocks/shadowsocks.git@master && \
    mkdir -p /etc/shadowsocks

EXPOSE 8388

ENTRYPOINT ["/usr/local/bin/ssserver"]
CMD ["-c", "/etc/shadowsocks/shadowsocks.json"]
